
<html>
<body>
<style>
table {border: none;}
</style>
<h2><b>sPARTA</b></h2>: small RNA-PARE Target Analyzer Version<br>
Updated: version-1.11 4/1/2015<br>
<br>
<h2><b>Description</b></h2><br>
small RNA-PARE Target Analyzer (sPARTA) is a tool which utilizes
high-throughput sequencing to profile genome-wide cleavage products.
sPARTA begins with a built-in parallelized target prediction module for plant
miRNAs called 'miRferno'. sPARTA as a whole utilizes multi-core servers to
achieve two-dimensional parallelization in order to maintain a low memory
footprint, imperative to achieve a full genome analysis. <br>
<br>
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
<br>
<h2><b>Note</b></h2><br>
1.sPARTA uses file extensions to identify file types, naming meta-data and selectively cleaning up temp files. Therefore, it is recommended to have appropriate file extensions.<br>
For Ex. a genome/cDNA FASTA file should have '.fa' extension.<br>
Please see 'Arguments' section (below) for recommended file extensions.<br>
<br>
2.Make sure that input fasta files do not have integers in name. For ex - test.1.fa or arabidopsis.new.2.4.fa<br>
Files with such names are deleted sometimes while cleanup operation<br>
<br>
3.All the input files 1) miRNAs 2) FASTA file for genome or transcripts and 3) degradome/PARE in tag-count format should be in same directory,including sPARTA script<br><br>

<h2><b>Execution</b></h2><br>
There are command line arguments that are to be used by sPARTA for proper
execution. For the first execution, all steps must be performed, but
once this has been completed, provided the miRNAs and genome are the same,
the entire analysis will not need to be repeated. Examples of such cases
may be seen below.<br>

<h2><b>Arguments</b></h2><br>
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>Month</th>
    <th>Savings</th>
  </tr>
  <tr>
    <td>January</td>
    <td>$100</td>
  </tr>
  <tr>
    <td>February</td>
    <td>$80</td>
  </tr>
</table>
<br>
<b>Genome and Annotation Data</b><br>
Both the GFF3 file and corresponding genome FASTA file can be downloaded from
Phytozome [http://www.phytozome.net/]<br>

<h2><b>Examples</b></h2><br>
<ol>
<li>Execution on new genome/entirely new dataset<br>
This execution should be performed any time a new genome file (along with corresponding GFF file) is being analyzed:<br>

python3 sPARTA.py -genomeFile <genomeFile.fa> -gffFile <GFF3file> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -libs <Lib_A.txt Lib_B.txt> -tarPred -tarScore --tag2FASTA --map2DD --validate<br>

OR<br>

a user provided feature set (FASTA file with sequences of interest) is being analyzed:<br>

python3 sPARTA.py -featureFile <featureFile.fa> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -libs <Lib_A.txt Lib_B.txt> -tarPred -tarScore --tag2FASTA --map2DD --validate</li><br>

<li>Execution on genome in which genome has already been processed<br>
This execution should be performed if a genome file has been processed previously but the miRNAs for which targets need to be predicted are new:<br>
<br>
python3 sPARTA.py -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -libs <Lib_A.txt Lib_B.txt> -tarPred -tarScore --tag2FASTA --map2DD --validate</li><br>

<li>Execution on data in which genome and miRNA files have been previously processed<br>
This execution should be performed if targets for a genome file have already been predicted using a miRNA file, but new PARE libraries need to be used for validation of earlier predicted targets:<br><br>

python3 sPARTA.py -genomeFeature <0/1> -libs <Lib_C.txt Lib_D.txt> --map2DD --validate</li><br>

<li>Execution of 'miRferno', just for target prediction<br>
This execution should be performed in case only predicted targets are required or PARE libraries are not available:<br>
python3 sPARTA.py -genomeFile <genomeFile.fa> -gffFile <GFF3file> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -tarPred -tarScore<br>

OR<br>

a user provided feature set (FASTA file with sequences of interest) is being analyzed:<br>

python3 sPARTA.py -featureFile <featureFile.fa> -genomeFeature <0/1> -miRNAFile <miRNAFile.fa> -tarPred -tarScore</li><br>
</ol>
<h2><b>Output</b></h2><br>
1.  PARE validation results for each library can be found in 'output' folder<br>
    under its corresponding library name. The 'output' folder also contains a combined result file (AllLibValidatedUniq.csv) from all the libraries.<br>
    Results from all libs were combined by removing redundant miRNA-target interaction with cleavage at same site.<br>
<br>
2.  Target prediction results can be found in 'predicted' folder under the name<br>
    'All.targs.parsed.csv'<br>

<h2><b>Contact</b></h2>
<br>
Atul Kakrana<br>
kakrana@udel.edu<br>

Reza Hammond<br>
hammond@dbi.udel.edu<br>

<b>END of README</b>
</body>
</html>
