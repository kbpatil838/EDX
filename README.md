# EDX
EDX INSTALLATION 

MAKE DOWNLOAD:-
==============

http://linuxpitstop.com/install-ubuntu-make-on-ubuntu-15-04/
===============================================================


Installing Ubuntu Make on Ubuntu 15.04

Installing “Ubuntu Make” is easy, launch your system terminal and run following command to add its PPA information to your package manager.



$ sudo apt-add-repository ppa:ubuntu-desktop/ubuntu-make
 _______________________________________________________

Now run following command to update your package manager repositories.


$ sudo apt-get update 
____________________



Install “Ubuntu Make” by running the following command:


$ sudo apt-get install ubuntu-make
__________________________________ 



Congratulations, Ubuntu Make is working on your Linux system now. Let’s see how we can install some commonly needed development applications using this tool.


__________________________________________________________________________________________________________
__________________________________________________________________________________________________________

Install using the repository :-
==============================

Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.
Set up the repository

Update the apt package index:


$ sudo apt-get update
---------------------

    
Install packages to allow apt to use a repository over HTTPS:

$ sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg-agent \
        software-properties-common
-------------------------------------


    
Add Docker’s official GPG key:

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
--------------------------------------------------------------------------------------


    Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.


$ sudo apt-key fingerprint 0EBFCD88
        
    pub   rsa4096 2017-02-22 [SCEA]
          9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
    uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
    sub   rsa4096 2017-02-22 [S]
-----------------------------------------------------------------------------


    Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.

Note: The lsb_release -cs sub-command below returns the name of your Ubuntu distribution, such as xenial. Sometimes, in a distribution like Linux Mint, you might need to change $(lsb_release -cs) to your parent Ubuntu distribution. For example, if you are using Linux Mint Tessa, you could use bionic. Docker does not offer any guarantees on untested and unsupported Ubuntu distributions.

        x86_64 / amd64
        armhf
        arm64
        ppc64le (IBM Power)
        s390x (IBM Z)

$ sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"
--------------------------------------------------------------------------



Install Docker CE :-
=====================

https://docs.docker.com/install/linux/docker-ce/ubuntu/
========================================================



Update the apt package index.


$ sudo apt-get update
------------------------


Install the latest version of Docker CE and containerd, or go to the next step to install a specific version:

    
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
------------------------------------------------------------


Got multiple Docker repositories?

        
If you have multiple Docker repositories enabled, installing or updating without specifying a version in the apt-get install or apt-get update command always installs the highest possible version, which may not be appropriate for your stability needs.

    
To install a specific version of Docker CE, list the available versions in the repo, then select and install:

    

a. List the versions available in your repo:

$ apt-cache madison docker-ce
------------------------------
      docker-ce | 5:18.09.1~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
      docker-ce | 5:18.09.0~3-0~ubuntu-xenial | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
      docker-ce | 18.06.1~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
      docker-ce | 18.06.0~ce~3-0~ubuntu       | https://download.docker.com/linux/ubuntu  xenial/stable amd64 Packages
      ...


b. Install a specific version using the version string from the second column, for example, 5:18.09.1~3-0~ubuntu-xenial.


$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
----------------------------------------------------------------------------------------------------



    
Verify that Docker CE is installed correctly by running the hello-world image.

    
$ sudo docker run hello-world
-------------------------------


_____________________________________________________________________________________________________
______________________________________________________________________________________________________


Step 1 — Installing Docker Compose :-
=======================================

https://www.digitalocean.com/community/tutorials/how-to-install-docker-compose-on-ubuntu-16-04
===============================================================================================


Although we can install Docker Compose from the official Ubuntu repositories, it is several minor version behind the latest release, so we'll install Docker Compose from the Docker's GitHub repository. The command below is slightly different than the one you'll find on the Releases page. By using the -o flag to specify the output file first rather than redirecting the output, this syntax avoids running into a permission denied error caused when using sudo.


We'll check the current release and if necessary, update it in the command below:


    
$ sudo curl -L https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
---------------------------------------------------------------------------------------------------


Next we'll set the permissions:

$ sudo chmod +x /usr/local/bin/docker-compose
----------------------------------------------

Then we'll verify that the installation was successful by checking the version:

$ docker-compose --version
-----------------------------


____________________________________________________________________________________________________
_____________________________________________________________________________________________________

3.3.2. Install Devstack :-
=============================

https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/installation/install_devstack.html
=======================================================


To install Devstack, follow these steps.

    Decide which branch you will be working with. “master” is the latest code in the repositories, changed daily. Open edX releases are more stable, for example, Hawthorn.


    
Check out a local copy of the edx/devstack repository from https://github.com/edx/devstack.

        
$ git clone https://github.com/edx/devstack
--------------------------------------------


    
Navigate to the devstack directory

        
cd devstack
----------

If you are not using the master branch, check out the branch you want.

        
$ git checkout open-release/hawthorn.master
-------------------------------------------


    
If you are not using the master branch, define an environment variable for the Open edX version you are using, such as hawthorn.master or zebrawood.rc1. Note that unlike a server install, the value of the OPENEDX_RELEASE variable should not use the open-release/ prefix.

        
$ export OPENEDX_RELEASE=hawthorn.master
----------------------------------------

    
Run make dev.checkout to check out the correct branch in the local checkout of each service repository.

        
$ make dev.checkout
----------------------


    
Clone the Open edX service repositories. The Docker Compose file mounts a host volume for each service’s executing code. The host directory defaults to be a sibling of the /devstack directory. For example, if you clone the edx/devstack repository to ~/workspace/devstack, host volumes will be expected in ~/workspace/course-discovery, ~/workspace/ecommerce, etc. You can clone these repositories with the following command.

        
$ make dev.clone
------------------

    
To customize where the local repositories are found, set the DEVSTACK_WORKSPACE environment variable.

    
(macOS only) Share the cloned service directories in Docker, using Docker -> Preferences -> File Sharing in the Docker menu.

   
 Run the provision command to configure the various services with superusers (for development without the auth service) and tenants (for multi-tenancy).

    
Note

    When you run the provision command, databases for ecommerce and edxapp will be dropped and recreated.

    

Use the following default provision command.

        
$ sudo make dev.provision
-----------------------------



_______________________________________________________________________________________________________
_____________________________________________________________________________________________________


                                SSO CONFIGURATION:
                               =====================

Register the Open edX Instance with Google:
============================================

1.Obtain credentials to access the Google API. To do this, follow the official Google instructions to go  to the Google Developers Console, create a new project, and enable the Google+ API service.

2.In the Google Developers Console, select API Manager, and then select OAuth Consent Screen.

3.For Product name shown to users enter the name of your Open edX instance (for example, “Example Academy Online”).

4.Select Save.

5.Select the Credentials tab, select Create credentials, and then select OAuth client ID.

    >For Application type, select Web application.

    >Leave the Authorized JavaScript origins field blank.
 
    >For Authorized redirect URIs, enter
          <Open edX instance domain>/auth/complete/google-oauth2/.
    
      For example, for devstack, enter http://localhost:8000/auth/complete/google-oauth2/.
    
    >Select Create to finish creating the credentials.

6.After you obtain the credentials, note the client ID and the client secret.




Configure Open edX:
===================

1. In the lms.env.json file, change the value of FEATURES > "AUTH_USE_OPENID_PROVIDER": true,
                                                            -----------------------------------
                                      ENABLE_THIRD_PARTY_AUTH to true (it is false by default). 
                                     -----------------------------------------------------------


2.In the lms.auth.json file, add the client secret. To do this, create the SOCIAL_AUTH_OAUTH_SECRETS key if the key does not already exist, and then add the appropriate value for your IdP.
   

       For Google, add the following value.
      -------------------------------------

          "SOCIAL_AUTH_OAUTH_SECRETS": { "google-oauth2":
                                                           "abcdef123456789101112131" }

       For Facebook, add the following value.
       --------------------------------------

           "SOCIAL_AUTH_OAUTH_SECRETS": {"facebook": "98765432181bbe3a2596efa8ba7abcde"}

       For LinkedIn, add the following value.
      ---------------------------------------

           "SOCIAL_AUTH_OAUTH_SECRETS": { "linkedin-oauth2": "4D3Cb2aB1C0dEFGH" }


       For Azure, add the following value.
      -------------------------------------

          "SOCIAL_AUTH_OAUTH_SECRETS": { "azuread-oauth2":
                                         "abcdef12341yHlmOrR8D3vlV1cD2VtL7k9xk9DSB8vw=" }


3. Restart the LMS server so that it will use the new settings.



Add the Provider Configuration:
================================

1.Go to <LMS URI>/admin/third_party_auth/oauth2providerconfig/. 
   For example, on devstack, go to http://localhost:8000/admin/third_party_auth/oauth2providerconfig/.
   
     id:edx  pswrd:edx (default)

2.Select Add Provider Configuration (OAuth).

3.Make sure that Enabled is selected.

4.Make sure that Visible is selected.

5.For Icon Class, enter the appropriate value.

          For Google, enter fa-google-plus.
          For Facebook, enter fa-facebook.
          For LinkedIn, enter fa-linkedin.
          For Azure, leave the field blank.
       
6.For Name, enter the appropriate value.

          For Google, enter Google.
          For Facebook, enter Facebook.
          For LinkedIn, enter LinkedIn.
          For Azure, enter Microsoft.
          
7.For Backend Name, select the appropriate value.

         For Google, select google-oauth2.
         For Facebook, select facebook.
         For LinkedIn, select linkedin-oauth2.
         For Azure, select azuread-oauth2.

8.For Client ID, enter the client ID that you noted earlie

9.For Client  Secret, enter the client  Secret that you noted earlie.

10.(Optional) If you want Facebook or LinkedIn to provide the user’s email address during registration, enter the following code into Other settings.


      For Facebook, use this code.

         {
             "SCOPE": ["email"],
             "PROFILE_EXTRA_PARAMS": {
               "fields": "id, name, email"
            }
         }



      For LinkedIn, use this code.

            { "SCOPE": ["r_basicprofile", "r_emailaddress"], "FIELD_SELECTORS":
                                  ["email-address"] }

11.Select Save.

______________________________________________________________________________________________________
________________________________________________________________________________________________________


                            XBLOCK INSTALLATION:
                            ====================
                            ====================

 Install XBlock Prerequisites:
==============================

To build an XBlock, you must have the following tools on your computer.

     Python 2.7
     Git
     A Virtual Environment


Create a Directory for XBlock Work:
=====================================

1. At the command prompt, run the following command to create the directory.

$ mkdir xblock_development
--------------------------

2. Change directories to the xblock_development directory.

$ cd xblock_development
------------------------

The rest of your work will be from this directory.



Create and Activate the Virtual Environment:
===========================================

1. At the command prompt in xblock_development, run the following command to create the virtual environment.

$ virtualenv venv
------------------

2. Run the following command to activate the virtual environment.

$ source venv/bin/activate
----------------------------


3. When the virtual environment is activated, the command prompt shows the name of the virtual directory in parentheses.

(venv) $
---------


Clone the XBlock Software Development Kit:
==========================================

1. In the xblock_development directory, run the following command to clone the XBlock SDK repository from GitHub.

(venv) $ git clone https://github.com/edx/xblock-sdk.git
--------------------------------------------------------

2. Run the following command to change to the xblock-sdk directory.

(venv) $ cd xblock-sdk
----------------------


3.Run the following command to install the XBlock SDK requirements.

(venv) $ pip install -r requirements/base.txt
---------------------------------------------

4. Run the following command to return to the xblock_development directory, where you will perform the rest of your work.

(venv) $ cd ..
----------------


Create an XBlock:
==================

1. Change to the xblock_development directory, which contains the venv and xblock-sdk subdirectories.

2. Run the following command to create the skeleton files for the XBlock.

(venv) $ xblock-sdk/bin/workbench-make-xblock
----------------------------------------------

Instructions in the command window instruct you to determine a short name and a class name. 

3. At the command prompt, enter the Short Name you selected for your XBlock.

$ Short name: myxblock
----------------------

4. At the command prompt, enter the Class name you selected for your XBlock.

$ Class name: MyXBlock
----------------------


Install the XBlock:
==================


After you create the XBlock, you install it in the XBlock SDK.

In the xblock_development directory, use pip to install your XBlock.

(venv) $ pip install -e myxblock
--------------------------------



Create the SQLite Database:
===========================

1. In the xblock_development directory, run the following command to create the database and the tables.

(venv) $ python xblock-sdk/manage.py migrate
---------------------------------------------

2. You are prompted to indicate whether or not to create a Django superuser.

You just installed Django's auth system, which means you don't have any
superusers defined. Would you like to create one now? (yes/no):

3. Enter no.

(venv) $ python no
-------------------



Run the XBlock SDK Server:
==========================

To see the web interface of the XBlock SDK, you must run the SDK server.

In the xblock_development directory, run the following command to start the server.

(venv) $ python xblock-sdk/manage.py runserver
-----------------------------------------------


Then test that the XBlock SDK is running. In a browser, go to http://localhost:8000. 
-------------------------------------------------------------------------------------



______________________________________________________________________________________________________
____________________________________________________________________________________________________






