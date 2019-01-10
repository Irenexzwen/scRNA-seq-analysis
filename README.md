# scRNA-seq Review 
*Auther: Xingzhao (Irene) Wen*
*Date: Jan 10th 2019*

>" Since then, many studies have focused on cell characterisation, redefining the cell, not only as structural, but also as functional unit of life " —— Arendt

**Table of Contents:**
[TOC]

## Introduction
It's good to be in a time that single cell transcriptom is easy to aquire with formulated protocols as well as good  to know these methods share certain brilliant commons that we can now easily follow up. 

It's been around a decade since [Tang et al., 2009](https://www.ncbi.nlm.nih.gov/pubmed/19349980) first proposed completely unbiased transcriptome-wide investigation of the mRNA in a single cell by taking advantage of high throughput DNA sequencing techonogy. Through years, technologies have been improved through **sensitivity, accuracy, cost efficiency and scalability.** 

&nbsp;

![2b9df47feda200bf61d723e78af74a14.png](en-resource://database/7729:1)@w=600
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *Figure 1 **Scaling of scRNA-seq experiments**. ([Svensson et al., 2018](https://www.nature.com/articles/nprot.2017.149))*


&nbsp;

All single cell RNA-seq protocols share a common initial step, where **transcribed RNA from cells can be converted to cDNA**. The next step is an **amplification**, using molecular biological methods such as polymerase chain reaction (PCR) or in vitro transcription (IVT). The subsequent steps, culminating in **sequencing** allow the expression level of gene products to be quantified. 

Most of these techniques can be categorized either based on  **amplification** method, namely:

*  PCR after polyA tailing
*  IVT (in vitro transcription) 
*  Template-switching

For most of the techniques direct or indirect derivation of these amplification method. I will walk though each method by its origin and applications for your better understanding. 

## scRNA-seq Techniques

### 1) PCR after polyA tailing 
Technologies in this category exploit the mRNA polyA tail and devise primer properly for later PCR amplification (exponential increase with potein more bias compared to other linear amplification method). 

#### Technique origin （Kurimoto 2006 )
In 2006, [Kurimoto et al.,](https://academic.oup.com/nar/article/34/5/e42/1146394) first proposed a method *"An improved single-cell cDNA amplification method for efficient high-density oligonucleotide microarray analysis"* . 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![b50f8dee260be5a6d9e8ba696bc3a1e4.png](en-resource://database/7733:1)@w=500


*Figure 2 **Schematic diagram of cDNA amplification**. The mRNA and cDNA are colored pink and orange, respectively. The V1, V3 and T7 promoter sequences are represented by blue, red and green boxes, respectively. The bars above the letters represent the complementary sequences.*

This protocol shows a paradiam for polyA tailing PCR amplification with few key steps to be noticed:

- Use V1 primer plus polyT to generate the first cDNA of template mRNA, and use Exonuclease I to digest unreacted primer. 

- **Add A at the end of first cDNA** and use **RNaseH** to digest RNA. (now, cDNA becomes template).

- Reverse transcribe the new template with a new V3+polyT primer to get double stranded cDNA. PCR for 20 cycles.

- Add T7 promoter PCR another 9 cycles. (**T7 promoter is used for transcribe cDNA template to RNA. RNAs are required for Affymetrix chip downstream analysis**). 


#### Technique applications and derivations:

##### a) sc mRNA-seq whole-stranscriptome (Tang 2009)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![1bdbcb11bbe1f5e76fd52d5e677aff4e.png](en-resource://database/7735:1)@w=500

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*Figure 3 **Schematic of the single-cell whole-transcriptome analysis.**[Tang et al., 2009](https://www.nature.com/articles/nmeth.1315)* 

This breakthrough work follows nearly the same idea as Kurimoto except for replacing array with sequencing (SOLiD system). Due to this reason, we could see that Tang didn't use T7 promoter any more. 

##### b) Quartz-seq 1&2 ([Sasagawa 2013](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2013-14-4-r31)) 
This method has been thoroughly reviewed by [Xiaochen](https://drive.google.com/open?id=1vq_mkT-UL1TcBkiynrfNDpDhMXEr2G_w). Quartz-seq include steps:

- Reverse transcription with an RT primer to generate the first-strand cDNAs from the target RNAs.

- The second step is a primer digestion with exonuclease I; this is one of the key steps to prevent the synthesis of byproducts.

- The third step is the addition of a poly-A tail to the 3’ ends of the first-strand cDNAs

- The fourth step is the second-strand synthesis using a tagging primer, which prepares the substrate for subsequent amplifi- cation. 

- The fifth step is a PCR enrichment reaction with a suppression PCR primer to ensure that a sufficient quantity ofDNA is obtained for the massively parallel sequencers or microarrays. All five steps are completed in **a single PCR tube** without any purification. 

![1e262fea44db5d0ce69efe914c7938da.png](en-resource://database/7739:1)@w=500
*Figure 4 Schematic of the whole-transcript amplification methods based on the poly-Atailing reaction* 

 **Main improvements** of Quartz-seq (compared to Kurimoto's method):
1) Achieved robust suppression of byproduct synthesis;
    
    -  **Exonuclease I**
    - **Suppression PCR** (byproduct cDNA is short which indicates a faster fasion for self hybridization. This short double strand cDNA is not subject to PCR amplification.) 
    ![5c88bfe4d72710cd5e1e8e1263e2f082.png](en-resource://database/7741:1)@w=500
    
    
2) Identified a robust PCR enzyme that allows the use of a single-tube reaction; 

    - MightyAmp DNA Polymerase

3) Determined the optimal conditions of reverse transcription (RT) and second-strand synthesis for the capturing mRNA and the first-strand cDNA.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![51cc5aeef9a48561f3fa1e5e0bc4862c.png](en-resource://database/7743:1)@w=400

Quartz-seq2 is a high throughput version of Quartz-seq1 combining Flow-cytometry into 384-well plate and cell barcode. 

![d23bec373ec27ce1ef5f705c941a87a2.png](en-resource://database/7747:1)

##### c) Other derivations:
![a67ae467471ac4e2e89a3d3352d5f15d.png](en-resource://database/7745:1)


### 2) In vitro transcription (IVT) amplification
#### Technique origin （Ebrewine 1992 )
IVT was first proposed by [Ebrewine et al., 1992](https://www.pnas.org/content/pnas/89/7/3010.full.pdf) and is a simple procedure that allows for template-directed synthesis of RNA molecules of any sequence from short oligonucleotides to those of several kilobases in μg to mg quantities. It is based on the engineering of a template that includes a bacteriophage promoter sequence (e.g. from the T7 coliphage) upstream of the sequence of interest followed by transcription using the corresponding RNA polymerase.

![6dbc6b35e754b9bf9fb5facbb73d69b8.png](en-resource://database/7749:1)@w=500 
*Figure 5 Schematic of the reamplification procedure used to achieve a millionfold amplification of the original RNA population from a single cell* 

Compared to PCR (which grows exponentially), IVT takes adavantage of using cDNA as template and use T7 promoter to transcribe. IVT will not be biased towards GC content since cDNA is of high fidelity. The shortage of this method is the efficiency of amplification( 200 copies/round ). However, later methods will combine IVT and PCR to achieve higher quantity and less errors. 


#### Technique applications and derivations:
![d9282ae58a3c60c9c1f9071cac413d7a.png](en-resource://database/7751:1)@w=700

##### a) CEL-Seq 1&2 (Hashimshony [2012](http://dx.doi.org/10.1016/j.celrep.2012.08.003) & [2016](http://dx.doi.org/10.1186/s13059-016-0938-8))
The CEL-Seq (Cell Expression by Linear amplification and Sequencing) protocol leveraged this for linear mRNA amplification from single cells. Here the RT adaptor also contains a T7 promoter, allowing the final double stranded DNA (dsDNA) to be transcribed into multiple copies of antisense RNA (aRNA). 

![22a8c0ca0b3de40deb48928e644214b3.png](en-resource://database/7753:1)@w=700 
*Figure 6 The CEL-Seq Method*

**Protocols**: 
1)  The CEL-Seq method begins with a single-cell reverse-tran scription reaction using a primer designed with an anchored polyT, a unique barcode, the 50 Illumina sequencing adaptor, and a T7 promoter.
2)  Second-strand synthesis is performed and then the cDNA samples are pooled(to obtain sufficient RNA from single cells for a single round of linear amplificatio) and consequently comprise sufficient template material for an IVT reaction. The amplified RNA is then subjected to directional RNA library preparation.
3)  The RNA is fragmented to a size distribution appropriate for sequencing, the Illumina 3' adaptor is added by ligation, RNA is reverse transcribed to DNA, and the 3'-most fragments that contain both Illumina adaptors and a barcode are selected. 
4)  The resulting library undergoes paired-end sequencing, where the first read recovers the barcode, whereas the second identifies the mRNA transcript. 

**Advantages**:
1)  Significantly reduced hands-on time both for the amplification and downstream pro- cessing (2- 3 days).
2)  The barcode is 8 bp in length and can be longer, the number of samples that may have unique barcodes in a given IVT is essentially unlimited. 
3)  Strand specificity (>98% of exonic reads come from the sense strand).

**Limitations**:
1)  The CEL-Seq protocol selects for the single 3'-most fragment of each transcript. In contrast to virtually all other RNA-Seq methods.
2)  Due to its strong 30 bias, the method is severely limited in its ability to distinguish alternative splice forms.

**CEL-Seq 2 is optimized for higher sensitivity**:
Seeking to improve CEL-Seq's efficiency, CEL-Seq2 introduced several changes:
![132b35ab6c6cb2396d35b8df5e75e525.png](en-resource://database/7755:1)
*Figure 7 Changes introduced to the protocol.* 

1)  Shortening the CEL-Seq primer from 92 to 82 nucleotides by reducing the length of the barcode from eight to six nucleotides, as well as shortening the T7 promoter and the Illumina 5'  adaptor.
2)  Optimized the conversion of RNA to dsDNA by testing alternative commercially available reverse transcriptases for cDNA synthesis and polymerases for second-strand synthesis namely **SuperScript II**.
3)  Modified our method of dsDNA and aRNA clean-up from column to beads.
4)  Ligation-free library preparation:  inserting the Illumina adaptor directly at the RT step as a5′-tail attached to a random hexamer, thus eliminating the ligation step and improves read mapping.
5)  Use UMI, high throughput. 
  

##### b) MARS-Seq (Jaitin [2014](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4412462/))

![c777e5a11a657b5d0c69cf07e8d573d4.png](en-resource://database/7757:1)@w=500

In short, MARS-Seq use the same 3' adaptor ligation method as CEL-Seq1 but different in Cell isolation method. 

##### c) inDrop-Seq (Klein [2015](http://dx.doi.org/10.1016/j.cell.2015.04.
The inDrop platform encapsulates cells into droplets with lysis buffer, reverse transcription(RT) reagents, and barcoded oligonucleotide primers. mRNA released from each lysed cell remains trapped in the same droplet and is barcoded during synthesis of cDNA. After barcoding, material from all cells is combined by breaking the droplets, and the cDNA library is sequenced using established methods **CEL-seq**.

The major challenge is to ensure that each droplet carries primers encoding a different barcode. People use droplet to capsule barcode with single cell using Droplet device.  

![f829e341be60ad663c4f85c63f85d8bd.png](en-resource://database/7763:1)
![aeed70dc92744b477f071019277f4081.png](en-resource://database/7765:1)
*Figure 8 Pipeline and Barcoding Hydrogel Microsphere Synthesis.* 



### 3) Template-switching PCR 

#### Technique origin 

From [wiki](https://en.wikipedia.org/wiki/Template_switching_polymerase_chain_reaction), the defination of TS-PCR is that:
> Template-switching polymerase chain reaction (TS-PCR) is a method of reverse transcription and polymerase chain reaction (PCR) amplification that relies on a natural PCR primer sequence at the polyadenylation site a.k.a. poly(A) tail, and adds a second primer through the activity of murine leukemia virus reverse transcriptase.[1] This permits reading full cDNA sequence and can deliver high yield from single sources, even single cells that contain 10 to 30 picograms of mRNA, with relatively low levels (3-5%) of contaminating rRNA sequence. 

A basic question is **the template is switching form what to what?**

To understand this question we could have a look at the figure from the first application of template switching application in single cell RNA sequencing **STRT-seq** ([Islam 2011](http://www.ncbi.nlm.nih.gov/pubmed/20859030)):

![325e6081bccd87516f717160658ad370.png](en-resource://database/7767:1)@w=500
*Figure 9 Single-cell tagged reverse transcription (STRT).* 

The key steps of template switching are that:
1)  Use olig-dT as primer to reverse transcribe target RNA to get the first cDNA strand with 3-6 added cytocines.
2)  Add template-switching oligonucleotide（TSO）primer (ii in green, which has a GGG at the beginning, **right now the template become the first cDNA strand**). The barcode is in green primer.
3)  The product is am- plified by single-primer PCR exploiting the template-suppression effect and is then immobilized on beads, fragmented, and A-tailed. 
4)  The Illumina P2 adapter (blue) is ligated to the free end.
5)  The P1 adapter is introduced in the library PCR step, using a primer tailed with the P1 se- quence (blue)
6)  The final library is sequenced from the P1 side using a custom primer.

As we could imagine, we could add barcode either at 3' or 5':
![a58e2b89f7c852a62ae983b0dcd822b7.png](en-resource://database/7769:0)@w=600
*Figure 9 TSO 3' or 5' scheme. [souce(10x genomics)](https://kb.10xgenomics.com/hc/en-us/articles/360001493051-What-is-a-template-switch-oligo-TSO-).*

Or we could not use barcode and build one library for each single cell to get the full length transcript which leads to SMART-Seq. 

To answer the question at the very beginning: **Polimerase does not switch strands, it switches from mRNA as a template to TSO as template.**

#### Technique applications and derivations:
##### a) Smart-Seq 1&2 ( Picelli [2014](https://www.nature.com/articles/nprot.2014.006) )

![532715c2d4c4416b13972dcd07f33afd.png](en-resource://database/7771:0)
*Figure 10 Flowchart for Smart-seq2 library preparation scheme.*

**Protocols:**
1)  Cell lysis: mild (hypotonic) lysis buffer contains free dNTPs and tailed oligo-dT oligonucleotides (30-nt poly-dT stretch and a 25-nt universal 5′ anchor sequence).
2)  RT reaction: using template-switching oligos(TSOs) and betaine with Mg2+ (overcome RNA secondary structures). Use polymerase Superscript II or KAPA HiFi. Temperature 50 °C for 2 min to promote unfolding of RNA secondary structures and then lower it to 42 °C for 2min to allow completion of RT. Repeat 10-15 cycles.
3)  template-switching reaction: M-MLV enzyme; Smart-seq2 uses a TSO carrying two riboguanosines in the third- and second-last positions and a modified guanosine to produce a locked nucleic acid (LNA) as the last base at the 3′ end which have 2 features: the enhanced thermal stability of the LNA monomers; and their ability to anneal strongly to the untemplated 3′ extension of the cDNA27.
4)  Tagmentation to quickly and efficiently construct sequencing libraries from the amplified cDNA. The tagmentation reaction takes advantage of a hyperactive derivative of the Tn5 transposase that catalyzes in vitro integration of predetermined oligonucleotides into target DNA29. The main advantage of this approach is that DNA fragmentation and adapter ligation occur in a single step, and size selection is not necessary. 
5) PCR. Fragments from previous step is of 200 - 600 bp. 

**Strengths**:
1)  Full-length cDNAs, It is therefore possible to analyze all the exons of each transcript and to detect the different splice variants, a big advantage over previous methods. It also enables comprehensive SNP and mutation analysis, widening its field of application.
2)  It allows a high degree of multiplexing; up to 96 samples can be pooled and sequenced on a single lane of an Illumina sequencer.

**Limitations**:
1)  Only valid for polyA tailed RNA.
2)  No strand-specific (because we have double-stranded cDNA before building library).
3)  Require a lot of labour for pooling samples. 

&nbsp;

##### b) Drop-Seq ( Macosko [2015](https://www.cell.com/abstract/S0092-8674(15)00549-8) )

![40486cd33d5cd989c110f5b46413ce9f.png](en-resource://database/7773:0)
*Figure 11 Extraction and Processing of Single-Cell Transcriptomes by Drop-Seq.*

##### c) SPLiT-Seq ( Rosenberg [2018](http://science.sciencemag.org/content/early/2018/03/14/science.aam8999.full))

Split-pool ligation-based transcriptome sequencing (SPLiT-seq) labels the cellular origin of RNA through combinatorial barcoding. It's cheap, require no additional equipment and efficient sample multiplexing. 

![20e1722885e28fd2c0ed60d11243f249.png](en-resource://database/7775:0)
*Figure 12 Labeling transcriptomes with split-pool barcoding. In each split-pool round, fixed cells or nuclei are randomly distributed into wells, and transcripts are labeled with well-specific barcodes. Barcoded RT primers are used in the first round. Second- and third-round barcodes are appended to cDNA through ligation. A fourth barcode is added to cDNA molecules by PCR during sequencing library preparation. The bottom schematic shows the final barcoded cDNA molecule.*

&nbsp;

![b4d383706f57802fedfcbb0d94f35b9b.png](en-resource://database/7777:0)
![618e3887c5cee70782f58a708ebdf822.png](en-resource://database/7779:0)
![dea831fa0c70fe03cda8384923928a41.png](en-resource://database/7781:0)

## Summary
### 1) Techniques combinations:
If we go over single cell sequencing workflow and details of each method:
![303ae0aff0ed6a555053c8e622fba7a0.png](en-resource://database/7791:0)
We would find there are three main parts that varies in different methods:

* **Cell isolation**
* **Primer types**
* **Reverse transcribe from mRNA to cDNA**

Every method is a combination of building blocks, will ou propose noval combinations?:
![3f51dd0c54eebfef3033fd1ef17d2044.png](en-resource://database/7797:0)



### 2) Comparative analysis of different methods:

Here we summarize the findings of benchmarking work from [Ziegenhain et al., 2017](10.1016/j.molcel.2017.01.023). 
#### Background
**Materials**: 583 mouse embryonic stem cells. All libraries were sequenced to a reasonable level of saturation at one million reads.
&nbsp;
**Technical Variable**:
1)  **Sensitivity**:  the probability to capture and convert a particular mRNA transcript present in a single cell into a cDNA molecule present in the library.
2)  **Accuracy**:  how well the read quantification corresponds to the actual concentration of mRNAs.
3)  **Precision**: the precision with which this amplification occurs (i.e., the technical variation of the quantification).
4)  **Cost**

![8f99051d120746d1570dea5105bc437d.png](en-resource://database/7783:0)
*Figure 13 Library preparation and features of six methods..*

#### Results
##### A) Number of genes detected (Sensitivity):

![00408c2c7bac899848a8edd30688a3fc.png](en-resource://database/7785:0)
*Figure 14 Sensitivity of scRNA-Seq Methods.*

* Smart-seq2 detected the highest number of genes per cell with a median of 9,138.
* Smart-seq2 is the most sensitive method, as it detects the highest number of genes per cell and the most genes in total across cells and has the most even coverage across transcripts.

##### B) Accuracy of scRNA-Seq Methods:
compared the observed expression values (counts per million or UMIs per million) with the known concentrations of the 92 **ERCC** transcripts. For each cell, we calculated the coefficient of determination (R2) for a linear model fit. Still, Smart-Seq2 achieves the best performance.

![5acb656ad0cf16c44e17f76f58ab07d1.png](en-resource://database/7787:0)@w=500
*Figure 15 Sensitivity of scRNA-Seq Methods. ERCC expression values (counts per million reads for Smart-seq/C1 and Smart-seq2 and UMIs per million reads for all others) were correlated to their annotated molarity. Shown are the distributions of correlation coefficients (adjusted R2 of linear regression model) across methods. Each dot represents a cell/bead and each box represents the median and first and third quartiles.*

##### C) Precision of Amplified Genes Is Strongly Increased by UMIs:
While a high accuracy is necessary to compare absolute expression levels, one of the most common experimental aims is to compare relative expression levels to identify differentially ex- pressed genes or different cell types.

Technical variation is substantial in scRNA-seq data primarily because a substantial fraction of mRNAs is lost during cDNA generation and small amounts of cDNA get amplified. Therefore, both the dropout probability and the amplification noise need to be considered when quantifying variation.

Smart-seq2 detects the common set of 13,361 genes in more cells than the UMI methods, but it has, as expected, more amplification noise than the UMI-based methods (Upon deep sequencing, each UMI will be observed multiple times, and the number of original DNA molecules can be determined simply by counting each UMI only once). 

##### D) Cost efficiency:
![7c6ccdf6ffe69b13ea65170a0e0cd2da.png](en-resource://database/7789:0)









































