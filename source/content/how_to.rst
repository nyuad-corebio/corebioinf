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


Dearchival of Data -> WIP
^^^^^^^^^^^^^^^^^^^^^^^^^

This procedure explains how to dearchive the data from archive node on jubail.     


.. _cgsb_miso:

Introduction to Lims - Miso -> WIP
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This procedure explains how to start with miso lims system to process your seqential runs. 

To request an account, please fill out this `form <https://docs.google.com/forms/d/e/1FAIpQLSfx3CxLrFb7FRh0hZlUfy2V-n85u1OTxSKngCoCzqyEs9psNQ/viewform>`__

Kindly refer to the video link below 

IGV -> WIP
^^^^^^^^^^

R-Studio loading libraries -> WIP
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

HPC Bioinfomatcis Software Stack
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


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
