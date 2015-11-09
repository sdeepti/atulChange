<html>
<body>
<h2>sPARTA</h2>
sPARTA: small RNA-PARE Target Analyzer Version<br> 
Updated: version-1.11 4/1/2015
<h2><b>Description</b></h2>
<p>small RNA-PARE Target Analyzer (sPARTA) is a tool which utilizes
high-throughput sequencing to profile genome-wide cleavage products.
sPARTA begins with a built-in parallelized target prediction module for plant
miRNAs called 'miRferno'. sPARTA as a whole utilizes multi-core servers to
achieve two-dimensional parallelization in order to maintain a low memory
footprint, imperative to achieve a full genome analysis. </p>
<h2><b>Dependencies</b></h2><br>
<b>sPARTA</b> requires bowtie2 in the PATH variable of the user account executing sPARTA<br>
bowtie2 may be downloaded here http://bowtie-bio.sourceforge.net/bowtie2/index.shtml<br>

sPARTA requires the following python3 functions to perform properly:<br>
numpy - http://www.numpy.org/<br>
pyfasta - https://pypi.python.org/pypi/pyfasta/<br>
rpy2 - http://rpy.sourceforge.net/<br>
scipy - http://www.scipy.org/<br>
<br>
These may easily be installed using (Python) PIP. Intructions to install PIP - https://pip.pypa.io/en/stable/installing.html<br>
<h2><b>Note</b></h2>
<ol>
<li>sPARTA uses file extensions to identify file types, naming meta-data and selectively cleaning up temp files. Therefore, it is recommended to have appropriate file extensions.<br>
For Ex. a genome/cDNA FASTA file should have '.fa' extension.<br>
Please see 'Arguments' section (below) for recommended file extensions.</li><br>
<li>Make sure that input fasta files do not have integers in name. For ex - test.1.fa or arabidopsis.new.2.4.fa<br>
Files with such names are deleted sometimes while cleanup operation</li><br>
<li>All the input files 1) miRNAs 2) FASTA file for genome or transcripts and 3) degradome/PARE in tag-count format should be in same directory,including sPARTA script</li>
</ol>
<h2><b>Execution</b></h2>
<p>There are command line arguments that are to be used by sPARTA for proper
execution. For the first execution, all steps must be performed, but
once this has been completed, provided the miRNAs and genome are the same,
the entire analysis will not need to be repeated. Examples of such cases
may be seen below.</p>
<h2><b>Arguments</b></h2><br>
<table border="0" class="nothing">
<tr>
<td>-gffFile</td>        
<td>GFF3 file for the species being analyzed corresponding  to the genome assembly being used. Recommended file
 extension - '.gff' or '.gff3'</td>
</tr>
<tr>
<td>-genomeFile</td>      
<td>Genome file in FASTA format that will be used to extract features (genic or intergenic regions) using GFF3 file.
Recommended file extension - '.fa'</td>
</tr>
<td>-featureFile</td>
<td>FASTA file containing sequences of interest (CDS, transcript,
 intergenic regions etc.) if user already has a set of
 sequences. This option is mutually exclusive to genome file and
gff file. So either genomefile along with gffFile is used or
 feature set is supplied directly. Recommended file extension - '.fa'</td>
</tr>
<tr><td>-genomeFeature</td>
<td>0 if prediction is to be done in genic region. 1 if prediction
... is to be done in intergenic region</td>
</tr>
<tr><td>-miRNAFile</td><td> FASTA format of miRNA sequences. Recommended file extension - '.fa'</td></tr>
<tr><td>-tarPred</td><td>Mode of target prediction. H for heuristic. E for exhaustive.
 H is default if no mode is specified</td></tr>
<tr><td>-tarScore</td><td>Scoring mode for target prediction. S for seedless. N for
normal. S is default if no mode is specified</td></tr>
<tr><td>-libs</td><td> List of PARE library files in tag count format. Data can be
 easily converted into tag count format using *********</td></tr>
<tr><td>-tagLen</td>       
<td> Minimum length of PARE tag, tags longer than tagLen will be
chopped to the specified length. 20 is default</td></tr>
<tr><td>--tag2FASTA</td>  
<td>Convert tag count file for PARE libraries to FASTA files for
mapping</td></tr>
<tr><td>--map2DD</td>
<td> Map the PARE reads to feature set</td>
<tr><td>--validate</td> 
<td>Flag to perform the validation of the potential cleave sites
 from miRferno</td></tr>
<tr><td>--repeats</td>      
<td> Flag to include PARE reads from repetitive regions</th></td></tr>
<tr><td>--noiseFilter</td>
<td> Flag to include all PARE validations with p-value of <=.5,
...             irrespective of the noise to signal ratio at cleave site and
...             category of PARE read.</td></tr>
<tr><td>-accel</td> 
<td>Y to use balanced multiple process scheme or else specify the
...             number of processors to be used. Y is default</td></tr>
</table>
<br>
<h2><b>Genome and Annotation Data</b></h2>
Both the GFF3 file and corresponding genome FASTA file can be downloaded from
Phytozome [http://www.phytozome.net/]<br>
</body>
</html>

```
python3 sPARTA.py -featureFile <featureFile.fa> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -libs <Lib_A.txt Lib_B.txt> -tarPred -tarScore --tag2FASTA --map2DD --validate</li><br>
```
<li>Execution on genome in which genome has already been processed<br>
This execution should be performed if a genome file has been processed previously but the miRNAs for which targets need to be predicted are new:<br>
<br>
```
python3 sPARTA.py -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -libs <Lib_A.txt Lib_B.txt> -tarPred -tarScore --tag2FASTA --map2DD --validate</li><br>
```

<li>Execution on data in which genome and miRNA files have been previously processed<br>
This execution should be performed if targets for a genome file have already been predicted using a miRNA file, but new PARE libraries need to be used for validation of earlier predicted targets:<br><br>
```
python3 sPARTA.py -genomeFeature <0/1> -libs <Lib_C.txt Lib_D.txt> --map2DD --validate</li><br>
```
<li>Execution of 'miRferno', just for target prediction<br>
This execution should be performed in case only predicted targets are required or PARE libraries are not available:<br>
```
python3 sPARTA.py -genomeFile <genomeFile.fa> -gffFile <GFF3file> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -tarPred -tarScore<br>
```

OR<br>

a user provided feature set (FASTA file with sequences of interest) is being analyzed:<br>
```
python3 sPARTA.py -featureFile <featureFile.fa> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -tarPred -tarScore</li>
```
</ol>
<h2><b>Output</b></h2>
<ol>
<li><p>PARE validation results for each library can be found in 'output' folder<br>
    under its corresponding library name. The 'output' folder also contains a combined result file (AllLibValidatedUniq.csv) from all the libraries.<br>
    Results from all libs were combined by removing redundant miRNA-target interaction with cleavage at same site.</p></li>
<li><p>Target prediction results can be found in 'predicted' folder under the name<br>
`All.targs.parsed.csv`</p></li>
</ol>

<h2><b>Contact</b></h2>
Atul Kakrana<br>
kakrana@udel.edu<br>
Reza Hammond<br>
hammond@dbi.udel.edu<br>

<b>END of README</b>
</body>
</html>
