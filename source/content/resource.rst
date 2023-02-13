Resource Page
==============




.. dropdown::  HPC Bioinfomatcis Software Stack


 This section explains how to load modules under gencore/2. 

 To load gencore2 modules 

 .. code:: bash

     $ module load all 
     $ module load gencore/2 



 1) Specify the first two letter of the software, and hit tab twice and you may able to see the options of software.     
    In the below example, I searched for samtools package, I entered first two letter and hit tab button twice 

 .. code:: bash

     $ module load sa
       salmon/    samtools/  savage/

 2)  Good, now I can see there is a module for samtools under gencore/2. If you find the package and then to check if you require any specific version of samtools, 
     again issue tab button twice, you are able to see the versions. 

 .. code:: bash

     $ module load samtools/
       samtools/1.3.1  samtools/1.9

 3)  Great, now I can choose samtools module with version 1.3.1

 .. code:: bash

     $ module load samtools/1.3.1
       
 4)  To check the loaded modules in your current shell

 .. code:: bash

     $ module list


 If you unable to find a package which is not available in the gencore/2 list, you may proceed with sending an email to nyuad.cgsb.cb@nyu.edu by mentioning below pointers.

 * Software version
 * Github or Software download link
 * If required databases to be downloaded, specify the exact link, names etc... 


