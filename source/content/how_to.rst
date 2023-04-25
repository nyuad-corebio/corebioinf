HOWTO's
============

.. tip:: For questions please emails us at nyuad.cgsb.cb@nyu.edu 

.. contents:: 
    :local:

    
--------------------------------------------------



SSH key login to Jubail HPC
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This procedure how to login to Jubail HPC using ssh key based authentication. This means the password prompt never prompt once you hit the ssh login command.
This method is a secure way to connect to HPC by setting up private and public keys. For more details about SSH key authentication `link <https://www.ssh.com/academy/ssh/public-key-authentication>`__ .

This is tested on Mac/Linux based laptops.   

**Steps**

1) Launch the terminal app

2) Issue the command "ssh-keygen" on the command line. Then press enter for all the questions as per below.

.. code:: bash

    $ ssh-keygen
    
Below is the output of ssh-keygen of issuing by user named john.

.. code-block:: none

    $ ssh-keygen
      Generating public/private rsa key pair.
      Enter file in which to save the key (/Users/john/.ssh/id_rsa):
      Enter passphrase (empty for no passphrase):
      Enter same passphrase again:
      Your identification has been saved in /Users/john/.ssh/id_rsa
      Your public key has been saved in /Users/john/.ssh/id_rsa.pub
      The key fingerprint is:
      SHA256:q2nJMP4ozzd5jbX23Y2bjfuYQNdSjfFlVij5oOzQp8I john@ADUAED15308LPMX
      The key's randomart image is:
      +---[RSA 3072]----+
      |             ...*|
      |            + .*o|
      |         o . +. +|
      |        . + . .o |
      |       .So o. o .|
      |    o   E.+. . . |
      |   . + o.= ..    |
      |  ....Boo +  o O.|
      |   o+++o . .. X+=|
      +----[SHA256]-----+
 

3) Copy the ssh public key towards the Jubail HPC server using "ssh-copy-id" command, password needs to be enter once it is prompted.

.. code:: bash

    $ ssh-copy-id net-id@jubail.abudhabi.nyu.edu

Below is the output of copying the public key to jubail hpc server as user named john. 

.. code:: none

    $ ssh-copy-id john@jubail.abudhabi.nyu.edu
      /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/john/.ssh/id_rsa.pub"
      /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
      /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
      john@jubail.abudhabi.nyu.edu's password:

      Number of key(s) added:        1

      Now try logging into the machine, with:   "ssh 'john@jubail.abudhabi.nyu.edu'"
      and check to make sure that only the key(s) you wanted were added.
      

4) Login to jubail HPC, now you are able to login to Jubail using key based authentication without prompting any password.  

.. code:: bash

    $ ssh <net-id>@jubail.abudhabi.nyu.edu 

Below is the output of login command as user named john.

.. code:: bash

    $ ssh john@jubail.abudhabi.nyu.edu
      Access allowed by pam_access
      - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
      Welcome to Jubail!
   
      For documentation & examples: https://crc-docs.abudhabi.nyu.edu
      For support: nyuad.it.help@nyu.edu
      - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

5) This step is optional, if you wish to launch this ssh connection using a friendly name let's say just "jubail" you can refer to below steps.

* Create a file named config under .ssh directory on your home folder

.. code:: bash

    $ touch ~/.ssh/config

* Fill out the contents of config file as below. Replace the net-id with yours.
   You can use any friendly name, only thing to specify in the "Host" section. 

.. code:: bash

    Host jubail
        Hostname jubail.abudhabi.nyu.edu 
        User <net-id> 

* Launch a new terminal tab or windows and issue below command.    

.. code:: bash

    $ ssh jubail

Below is the output of login command with friendly name "jubail"

.. code:: bash

    $ ssh jubail
      Access allowed by pam_access
      - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
      Welcome to Jubail!

      For documentation & examples: https://crc-docs.abudhabi.nyu.edu
      For support: nyuad.it.help@nyu.edu
      - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

.. note:: If you want to setup ssh key based authentication on Windows laptop, kindly refer to this `link <https://www.mythic-beasts.com/support/topics/ssh-keys>`__



.. _cgsb_sftp:

Transfer files using  CGSB SFTP service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This procedure explains how to transfer files to external collaberators.

There are two ways you can transfer files to CGSB file transfer server

To request an account, please fill out this `form <https://docs.google.com/forms/d/e/1FAIpQLSeQ9A2yF2s0iFzVpCYr_aYneD-l4x_Y5iEMiGPxNIhaO9eOAA/viewform>`__

    

**1) Using Command Line**
   

Launch terminal app from your laptop
If data resides in jubail, you would need to login to jubail and follow below instruction. 

.. code:: bash

    $ rsync -av --progress -e 'ssh -p 4410' <local-path> <net-id>@cgsb-sftp.abudhabi.nyu.edu:<destination-path>

Below is an example, here i would like to share a directory named **datadir** from jubail to SFTP site on path **/data/jr5241/upload** 

.. code:: bash

    $ rsync -av --progress -e 'ssh -p 4410' /scratch/jr5241/datadir jr5241@cgsb-sftp.abudhabi.nyu.edu:/data/jr5241/upload/



**2) Using Filezilla** 
   


If the data resides in Jubail, then you need to login to `Jubail Web Interface <https://ood.hpc.abudhabi.nyu.edu>`__  . Then launch **Filezilla** GUI application from the **Interactive Apps** menu.     
If you have any doubts navigating to Jubail Web Interface, kindly refer to `NYUAD CRC page <https://crc-docs.abudhabi.nyu.edu/hpc/ood/index.html>`__ 

If the data resides locally then you need to download `Filezilla <https://filezilla-project.org/download.php?type=client>`__ on your laptop. 

Below information will share with you once you request for an sftp account

.. code-block:: none

    Host: sftp://cgsb-sftp.abudhabi.nyu.edu
    User: <net-id>
    Pass: <Specify the password shared with you>
    Port: 4410



.. figure::  /images/filezilla_login.png
   :align: center

   *Figure: Specifying Credentials*
 

.. figure::  /images/filezilla_copy.png
   :align: center

   *Figure: Transfer window between source and destination*

If you are unable to transfer data to the SFTP site, please write us nyuad.cgsb.cb@nyu.edu 


Dearchival of Data 
^^^^^^^^^^^^^^^^^^^

This procedure explains how to request for dearchive data from gencore archive node on jubail.  

* Send an email to nyuad.cgsb.cb@nyu.edu 
* Mention the jira ticket number.
* Specify the type of data you would require for eg:- raw data, qc fastq, raw counts etc..
* Specify the sample names, if possible. 

Based on the request, we will start dearchive the data from the archive node as follows:- 

Once login to jubail login node, and will issue the de-archive as follows.

To check the size of the de-archive directory.

.. code:: bash

    $dmfdu -d </archive/gencore/XXXX/XXXX/XXX>

To issue the de-archive command.

.. code:: bash 

    $ dmfget -d </archive/gencore/XXXX/XXXX/XXX>

To check the real time status of the dearchive process.

.. code:: bash 

    $ watch -n2 dmfmonitor -d </archive/gencore/XXXX/XXXX/XXX>


.. Tip:: How to understand the archive status:

     * released exists archived ->> unreadable state
     * exists archived ->> readable state

To check the state of dearchive directory.
If you need to check the status of file, remove the "-d" flag

.. code:: bash 

    $ dmfls -d </archive/gencore/XXXX/XXXX/XXX>


De-archive CGSB shared path
----------------------------

This shared space is only visible to the end user and cgsb core team. 
Below is the path of cgsb dearchive shared space.

.. code:: bash

    $ /scratch/share/cgsb

Create a net-id named directory. ( for eg:- if abc123 named user is the requester )

.. code:: bash

    $ mkdir /scratch/share/cgsb/abc123

Transfer the data to the shared space

.. code:: bash

    $ rsync -avP </archive/gencore/XXXX/XXXX/XXX> /scratch/share/cgsb/abc123

.. warning:: 
     * Once the data copied to the cgsb shared location, the ownership will change from gencore to respective users.
     * The copied files will consume space from the requested user quota.
     * Once the files copied in this location will be available for 2 weeks. Hence kindly remove the directory once you copied the files.
     * Once the storage quota reaches beyond your permitted value, you are unable to login to jubail node. In that case reach out to jubail support team.
     
    

.. _cgsb_miso:

Introduction to Lims - Miso
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This procedure explains how to start with miso lims system to process your seqential runs. 

To request an account, please fill out this `form <https://docs.google.com/forms/d/e/1FAIpQLSfx3CxLrFb7FRh0hZlUfy2V-n85u1OTxSKngCoCzqyEs9psNQ/viewform>`__

Kindly refer to the video link below 

.. raw:: html

   <iframe width="560" height="315" src="https://www.youtube.com/embed/vE5mFv-zMpk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

|

.. _cgsb_varseq:

Varseq
^^^^^^^

This procedure explains how to access on varseq server graphically. 

VarSeq is an intuitive, integrated software solution for tertiary analysis.

* VNC client software is needed on your laptop to access varseq. Refer to `Download link <https://www.realvnc.com/en/connect/download/viewer>`__
* VNC password is a local one and this can be generated as follows:- 

Login to varseq server and set a password after entering "vncpasswd" as below. This is a one time task.

.. code:: bash

    $ ssh -p 4410 <net-id>@varseq.abudhabi.nyu.edu 
    $ vncpasswd

To access VNC graphical interface, search for vnc client software on your laptop. Type the vnc url provided by varseq administrator. 
for eg:- varseq.abudhabi.nyu.edu:5910 , then it prompt a window to enter the vncpasswd which we created above.

To launch the application. 

.. code:: bash

    $ ssh -p 4410 <net-id>@varseq.abudhabi.nyu.edu 
    $ cd ~/Varseq
    $ ./VarSeq

To mount jubail path on varseq server as follows:-

.. code:: bash

    $ sshfs <net-id>@dalma.abudhabi.nyu.edu:<remote-path> <local-path>
    $ mkdir ~/jubail_share
    $ sshfs jr5241@jubail.abudhabi.nyu.edu:/scratch/jr5241 ~/jubail_share 

To unmount the mapping.

.. code:: bash

    $ fusermount -u  ~/jubail_share

Interactive Apps in Jubail Web GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This section shows the procedure how to load Bioinfomatics Web Interactive Apps from jubail.

IGV(Interactive Genomics Viewer)
---------------------------------

The Integrative Genomics Viewer (IGV) is a high-performance, easy-to-use, interactive tool for the visual exploration of genomic data.

To load this package in jubail Web Graphical Interface(GUI) as follows:

Click on this link https://ood.hpc.abudhabi.nyu.edu , enter your NetID and password and click Log in with your NYU account.

Click on "Interactive Apps" tabs and then select "IGV"


Cytoscape
---------

Cytoscape is an open source software platform for visualizing complex networks and integrating these with any type of attribute data.

To load this package in jubail Web Graphical Interface(GUI) as follows:

Click on this link https://ood.hpc.abudhabi.nyu.edu , enter your NetID and password and click Log in with your NYU account.

Click on "Interactive Apps" tabs and then select "Cytoscape"

Jalview
--------

Jalview is a free cross-platform program for multiple sequence alignment editing, visualisation and analysis.

To load this package in jubail Web Graphical Interface(GUI) as follows:

Click on this link https://ood.hpc.abudhabi.nyu.edu , enter your NetID and password and click Log in with your NYU account.

Click on "Interactive Apps" tabs and then select "Jalview"

R-Studio loading libraries 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We build R libraries for some packages in R v4.2.1, you can simply load this on your R-Studio/R on jubail. 

Launch Rstudio on HPC OOD GUI environment or you can load the R environment on your command line in jubail as follows.
Note:- If you install R on a different version, there will be some conflits. We recommend to stay in R v4.2.1

To load in jubail in CLI ( Command Line Interface )
.. code:: bash 

    module load gencore/1
    module load Miniconda3/4.7.10
    source activate /scratch/gencore/conda3/envs/RStudio

Seurat
--------

R toolkit for single cell genomics.

**a) 4.2.0**

.. code:: bash 

    .libPaths("/scratch/gencore/software/RStudio/Seurat/4.2.0")
    library("Seurat")

To verify the library path is set or not using 

.. code:: bash 

    .libPaths()

**b) 3.2.3**

.. code:: bash 

    .libPaths("/scratch/gencore/software/RStudio/Seurat/3.2.3")
    library("Seurat")

To verify the library path is set or not using 

.. code:: bash 

    .libPaths()

**c) 2.3.0**

.. code:: bash 

    .libPaths("/scratch/gencore/software/RStudio/Seurat/2.3.0")
    library("Seurat")

To verify the library path is set or not using

.. code:: bash 

    .libPaths()

Monocle
---------

R toolkit for single-cell RNA-Seq analysis.

**a) 2.26.0**

.. code:: bash 

    .libPaths("/scratch/gencore/software/RStudio/Monocle/2.26.0")
    library("monocle")

To verify the library path is set or not using 

.. code:: bash 

    .libPaths()

Dupradar
----------

R toolkit for duplication rates in RNA-Seq datasets.

**a) 1.28.0**

.. code:: bash 

    .libPaths("/scratch/gencore/software/RStudio/Dupradar/1.28.0")
    library("dupRadar")

To verify the library path is set or not using 

.. code:: bash 

    .libPaths()

HPC Bioinfomatics Software Stack
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

How we add packages in jubail 
------------------------------

We added packages in below methods. 

* Installed via easybuild ( eg:- module load samtools/1.9 )
* Installed via conda environment ( eg:- source activate /scratch/gencore/conda3/envs/repeatmasker4.1.5 )
* Installed via compiling from source ( eg:- Using the tar.gz of the package )
* Installed via singularity in jubail ( this is still experimental )
* Installed via Docker on our annotation server. 


Loading package using conda 
----------------------------

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

Loading package using "source activate <package-path>"
-------------------------------------------------------

This section explains how to load packages under conda.
In the below example, using Miniconda module, you are enabling the repeatmasker 4.1.5 verison as a conda environment on your path.

.. code:: bash
    
    $ module load gencore/1
    $ module load Miniconda3/4.7.10
    $ source activate /scratch/gencore/conda3/envs/repeatmasker4.1.5


Loading package from sources
--------------------------------------------------

This section explains how to load packages source path location. 
Compiled packages are available under below path.

.. code:: bash

   $ /scratch/gencore/software/

To load the specified package path, for eg:- maker version 2, you may issue below command in your command line.

.. code:: bash

    $ export PATH='/scratch/gencore/software/maker2':$PATH

To request a package 
--------------------

If you unable to find a package, you may proceed with sending an email to nyuad.cgsb.cb@nyu.edu by mentioning below pointers.

* Software version
* Github or Software download link
* If required databases to be downloaded, specify the exact link, names etc... 


Documentation of packages 
^^^^^^^^^^^^^^^^^^^^^^^^^

This section explains the install method for some packages which will be installed from source with many dependencies. 

Repeatmasker
------------

RepeatMasker is a program that screens DNA sequences for interspersed repeats and low complexity DNA sequences.
This installation procedure is based on v4.1.5

Reference:- https://www.repeatmasker.org/RepeatMasker/

Download repeatmasker version 4.1.5 from this `link <https://www.repeatmasker.org/RepeatMasker/RepeatMasker-4.1.5.tar.gz>`__

Copy the downloaded file to the install location and extract in jubail.

.. code:: bash

    $ cp RepeatMasker-4.1.5.tar.gz /scratch/gencore/softwares/
    $ cd /scratch/gencore/softwares/
    $ tar -xvf RepeatMasker-4.1.5.tar.gz
    $ mv RepeatMasker RepeatMasker-4.1.5

Then we would need to install the prerequisites for building this package. We can accomplish this by using the anaconda. 

.. code:: bash

    $ module load gencore/1
    $ module load Miniconda3/4.7.10
    $ conda create -p /scratch/gencore/conda3/envs/repeatmasker4.1.5 -c conda-forge -c bioconda hmmer rmblast trf bioawk -y
    $ source activate /scratch/gencore/conda3/envs/repeatmasker4.1.5

Place the RepBase RepeatMasker Edition ( final version 10/26/2018 )  in the install directory and extract the contents.

.. code:: bash

    $ cp /scratch/Reference_Genomes/Public/RepeatMasker/RepBaseRepeatMaskerEdition-20181026.tar.gz /scratch/gencore/softwares/RepeatMasker-4.1.5/
    $ cd /scratch/gencore/softwares/RepeatMasker-4.1.5/
    $ tar -xvf RepBaseRepeatMaskerEdition-20181026.tar.gz

Download the Dfam 3.7 Library from this `link <https://www.dfam.org/releases/Dfam_3.7/families/Dfam.h5.gz>`__ and extract the contents to the Libraries directory.

.. code:: bash

    $ cp /scratch/Reference_Genomes/Public/RepeatMasker/Dfam.h5.gz /scratch/gencore/softwares/RepeatMasker-4.1.5/
    $ gunzip Dfam.h5.gz
    $ mv Dfam.h5 Libraries/

Run the Configure script as follows:-

.. code:: bash

    $ perl ./configure -libdir /scratch/gencore/software/RepeatMasker-4.1.5/Libraries -trf_prgm /scratch/gencore/conda3/envs/repeatmasker4.1.5/bin/trf 
    -rmblast_dir /scratch/gencore/conda3/envs/repeatmasker4.1.5/bin/ -hmmer_dir /scratch/gencore/conda3/envs/repeatmasker4.1.5/bin 
    -abblast_dir /scratch/gencore/conda3/envs/repeatmasker4.1.5/bin -crossmatch_dir /scratch/gencore/conda3/envs/repeatmasker4.1.5/bin 
    -default_search_engine rmblast

Great, you may see below message once the setup is done.

.. code:: bash

    Building FASTA version of RepeatMasker.lib ......................................................................
    Building RMBlast frozen libraries..
    The program is installed with a the following repeat libraries:
    File: /scratch/gencore/software/RepeatMasker-4.1.5/Libraries/RepeatMaskerLib.h5
    FamDB Generator: famdb.py v0.4.2
    FamDB Format Version: 0.5
    FamDB Creation Date: 2023-01-08 10:42:05.645898

    Database: Dfam withRBRM
    Version: 3.7
    Date: 2023-01-11

To load the modules, follow below procedure.

Launch a new session in jubail.

.. code:: bash

    $ module load gencore/1
    $ module load Miniconda3/4.7.10
    $ source activate /scratch/gencore/conda3/envs/repeatmasker4.1.5
    $ export PATH='/scratch/gencore/software/RepeatMasker-4.1.5:/scratch/gencore/software/RepeatMasker-4.1.5/util':$PATH

Maker
-----

MAKER is a portable and easily configurable genome annotation pipeline.
Its purpose is to allow smaller eukaryotic and prokaryotic genome projects to independently annotate their genomes and to create genome databases.

This is based on Maker version 3.01.04
Reference:- https://www.yandell-lab.org/software/maker.html

Prerequisites

.. code:: bash

    blast - 2.13.0
    snap - 2013_11_29
    exonerate - 2.4.0
    genblasta - 1.0.4
    RepeatMasker - 4.1.2.p1
    snoscan - 1.0 
    trnascan-se - 2.0.9
    interproscan - 5.55_88.0

.. code:: bash

    $ module load gencore
    $ module load Miniconda3/4.7.10
    $ conda create -p /scratch/gencore/conda3/envs/maker3 -c conda-forge perl=5.26.2
    $ source activate /scratch/gencore/conda3/envs/maker3
    $ wget http://weatherby.genetics.utah.edu/maker_downloads/D2BE/7CA3/067C/DC399810E1834576C76C4203FC4A/maker-3.01.04.tgz

Extract the file and switch to build directory which is ../maker/src/ and execute "perl Build.PL" to check the list of dependencies.

.. code:: bash

    $ tar -xvf maker-3.01.04.tgz
    $ cd maker/src/
    $ perl Build.PL

Below commands solves perl dependencies

.. code:: bash

    $ conda install -c bioconda   perl-io-all perl-inline-c
    $ conda install -c bioconda perl-forks perl-want perl-bit-vector perl-bit-vector perl-dbd-sqlite perl-perl-unsafe-signals perl-dbd-pg
    $ conda install -c bioconda   perl-bioperl-core

Below commands solves external softwares like blast, snap, exonerate etc..

.. code:: bash

    $ conda install -c bioconda snap exonerate blast
    $ conda install -c bioconda snoscan trnascan-se interproscan
    $ conda install -c bioconda repeatmasker

Note:- if conda for repeatmasker fails, try below 

.. code:: bash

    $ ./Build installexes 
    $ conda install -c bioconda genblasta
    $ conda install -c bioconda blast-legacy 

Preparing the environment, you may see below message. 

.. code:: bash

    $ perl Build.PL
    ==============================================================================
    STATUS MAKER v2.31.11
    ==============================================================================
    PERL Dependencies:	VERIFIED
    External Programs:	VERIFIED
    External C Libraries:	VERIFIED
    MPI SUPPORT:		DISABLED
    MWAS Web Interface:	DISABLED
    MAKER PACKAGE:		CONFIGURATION OK

To build the installation proceed below 

.. code:: bash

    $ ./Build install
    Building MAKER
    Installing MAKER...
    Building MAKER
    Installing /scratch/gencore/software/maker2/src/../perl/lib/MAKER/ConfigData.pm
    Installing /scratch/gencore/software/maker2/src/../perl/lib/Parallel/Application/MPI.pm
    Installing /scratch/gencore/software/maker2/src/../perl/man/MAKER::ConfigData.3
    Installing /scratch/gencore/software/maker2/src/../bin/map_data_ids
    Installing /scratch/gencore/software/maker2/src/../bin/maker_map_ids
    Installing /scratch/gencore/software/maker2/src/../bin/fasta_tool
    Installing /scratch/gencore/software/maker2/src/../bin/iprscan2gff3
    Installing /scratch/gencore/software/maker2/src/../bin/genemark_gtf2gff3
    Installing /scratch/gencore/software/maker2/src/../bin/maker_functional_gff
    Installing /scratch/gencore/software/maker2/src/../bin/chado2gff3
    Installing /scratch/gencore/software/maker2/src/../bin/tophat2gff3
    Instruction to run maker2 as normal user
    ===

To load the maker package.

.. code:: bash


  $  module load gencore
  $  module load Miniconda3/4.7.10
  $  source activate /scratch/gencore/conda3/envs/maker3
  $  export PATH="/scratch/gencore/.eb/2.0/software/augustus/3.4.0/bin:$PATH"
  $  export PATH="/scratch/gencore/software/gmes_linux_64:$PATH"
  $  export PATH="/scratch/gencore/software/ab-blast:$PATH"
  $  export PATH="/scratch/gencore/software/genemark_prokaryotic:$PATH"
  $  export PATH="/scratch/gencore/software/maker3/bin:$PATH"
  $  maker -h

Database location for Maker

.. code:: bash

    $ /scratch/Reference_Genomes/Public/maker2_datasets/



Anvio
------

Anvi’o is a comprehensive platform that brings together many aspects of today’s cutting-edge computational strategies of data-enabled microbiology,
including genomics, metagenomics, metatranscriptomics, pangenomics, metapangenomics, phylogenomics, and microbial population genetics in an integrated
and easy-to-usefashion through extensive interactive visualization capabilities.

Anvio can be install using conda as follows and this is based on version 7.1
Reference:- https://anvio.org/

.. code:: bash

    $ conda create -p /scratch/gencore/conda3/envs/anvio-7  python=3.6 -y
    $ source  activate /scratch/gencore/conda3/envs/anvio-7
    $ conda install -y -c bioconda "sqlite>=3.31.1"
    $ conda install -y -c bioconda prodigal
    $ conda install -y -c bioconda mcl
    $ conda install -y -c bioconda muscle=3.8.1551
    $ conda install -y -c bioconda hmmer
    $ conda install -y -c bioconda diamond
    $ conda install -y -c bioconda blast
    $ conda install -y -c bioconda megahit
    $ conda install -y -c bioconda spades
    $ conda install -y -c bioconda bowtie2 tbb=2019.8
    $ conda install -y -c bioconda bwa
    $ conda install -y -c bioconda samtools=1.9
    $ conda install -y -c bioconda centrifuge
    $ conda install -y -c bioconda trimal
    $ conda install -y -c bioconda iqtree
    $ conda install -y -c bioconda trnascan-se
    $ conda install -y -c bioconda r-base
    $ conda install -y -c bioconda r-stringi
    $ conda install -y -c bioconda r-tidyverse
    $ conda install -y -c bioconda r-magrittr
    $ conda install -y -c bioconda r-optparse
    $ conda install -y -c bioconda bioconductor-qvalue
    $ conda install -y -c bioconda fasttree
    $ conda install -y -c bioconda vmatch
    $ conda install -y -c bioconda fastani

Then download anvio package as follows:- 

.. code:: bash

    $ curl -L https://github.com/merenlab/anvio/releases/download/v7.1/anvio-7.1.tar.gz   
    $ pip install anvio-7.1.tar.gz

