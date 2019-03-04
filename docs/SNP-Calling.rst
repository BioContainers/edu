
----

title: 'SNP Calling'
layout: series_item
series: 'containers-examples'
permalink: /containers-examples/SNP-Calling/

estimated-time: 5
-----------------

.. code-block::


   #http://www.htslib.org/workflow/#mapping_to_variant
   set -xeu

   FQ1=y1.fastq
   FQ2=y2.fastq
   REF=yeast.fasta
   BNM=yeastD

   RUNINDOCKER=1

   SAMTOOLS=samtools
   BWA=bwa
   TABIX=tabix
   BCFTOOLS=bcftools
   PLOTVCFSTATS=plot-vcfstats

   if [[ "$RUNINDOCKER" -eq "1" ]]; then
   echo "RUNNING IN DOCKER"
   DRUN="docker run --rm -v $PWD:/data --workdir /data -i"
   #--user=biodocker

   SAMTOOLS_IMAGE=/samtools
   BWA_IMAGE=/bwa
   TABIX_IMAGE=dev/htslib:1.2.1
   BCFTOOLS_IMAGE=/bcftools


   docker pull $SAMTOOLS_IMAGE
   docker pull $BWA_IMAGE
   docker pull $TABIX_IMAGE
   docker pull $BCFTOOLS_IMAGE

   SAMTOOLS="$DRUN $SAMTOOLS_IMAGE $SAMTOOLS"
   BWA="$DRUN $BWA_IMAGE $BWA"
   TABIX="$DRUN $TABIX_IMAGE $TABIX"
   BCFTOOLS="$DRUN $BCFTOOLS_IMAGE $BCFTOOLS"
   PLOTVCFSTATS="$DRUN $BCFTOOLS_IMAGE $PLOTVCFSTATS"
   else
   echo "RUNNING LOCAL"
   fi

   HEADLEN=100000

   if [[ ! -f "$FQ1" ]]; then
   curl ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR507/SRR507778/SRR507778_1.fastq.gz| gzip -d | head -$HEADLEN > $FQ1.tmp && mv $FQ1.tmp $FQ1
   fi

   if [[ ! -f "$FQ2" ]]; then
   curl ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR507/SRR507778/SRR507778_2.fastq.gz| gzip -d | head -$HEADLEN > $FQ2.tmp && mv $FQ2.tmp $FQ2
   fi

   if [[ ! -f "$REF" ]]; then
   curl ftp://ftp.ensembl.org/pub/current_fasta/saccharomyces_cerevisiae/dna/Saccharomyces_cerevisiae.R64-1-1.dna_sm.toplevel.fa.gz | gunzip -c > $REF.tmp && mv $REF.tmp $REF
   fi

   if [[ ! -f "$REF.fai" ]]; then
   $SAMTOOLS faidx $REF
   fi

   if [[ ! -f "$REF.bwt" ]]; then
   $BWA index $REF
   fi

   if [[ ! -f "$BNM.sam" ]]; then
   $BWA mem -R '@RG\tID:foo\tSM:bar\tLB:library1' $REF $FQ1 $FQ2 > $BNM.sam.tmp && mv $BNM.sam.tmp $BNM.sam
   fi

   if [[ ! -f "$BNM.bam" ]]; then
   #$SAMTOOLS sort -O bam -T /tmp -l 0 --input-fmt-option SAM -o $BNM.tmp.bam $BNM.sam && mv $BNM.tmp.bam $BNM.bam
   $SAMTOOLS sort -O bam -T /tmp -l 0 -o $BNM.tmp.bam $BNM.sam && mv $BNM.tmp.bam $BNM.bam
   fi

   if [[ ! -f "$BNM.cram" ]]; then
   $SAMTOOLS view -T $REF -C -o $BNM.tmp.cram $BNM.bam && mv $BNM.tmp.cram $BNM.cram
   fi

   if [[ ! -f "$BNM.P.cram" ]]; then
   $BWA mem $REF $FQ1 $FQ2 | \
   $SAMTOOLS sort -O bam -l 0 -T /tmp - | \
   $SAMTOOLS view -T $REF -C -o $BNM.P.tmp.cram - && mv $BNM.P.tmp.cram $BNM.P.cram
   fi

   #if [[ ! -f "" ]]; then
   #$SAMTOOLS view $BNM.cram
   #fi

   #if [[ ! -f "" ]]; then
   #$SAMTOOLS mpileup -f $REF $BNM.cram
   #fi

   if [[ ! -f "$BNM.vcf.gz" ]]; then
   $SAMTOOLS mpileup -ugf $REF $BNM.bam | $BCFTOOLS call -vmO z -o $BNM.vcf.gz.tmp && mv $BNM.vcf.gz.tmp $BNM.vcf.gz
   fi

   if [[ ! -f "$BNM.vcf.gz.tbi" ]]; then
   $TABIX -p vcf $BNM.vcf.gz
   fi

   if [[ ! -f "$BNM.vcf.gz.stats" ]]; then
   $BCFTOOLS stats -F $REF -s - $BNM.vcf.gz > $BNM.vcf.gz.stats.tmp && mv $BNM.vcf.gz.stats.tmp $BNM.vcf.gz.stats
   fi

   mkdir plots &>/dev/null || true

   #if [[ ! -f "plots/tstv_by_sample.0.png" ]]; then
   #$PLOTVCFSTATS -p plots/ $BNM.vcf.gz.stats
   #fi

   if [[ ! -f "$BNM.vcf.filtered.gz" ]]; then
   $BCFTOOLS filter -O z -o $BNM.vcf.filtered.gz -s LOWQUAL -i'%QUAL>10' $BNM.vcf.gz
   fi
