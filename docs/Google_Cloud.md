**Foreword**

This step-by-step tutorial to set up a data science environment on Google Cloud: create an instance on Google Compute Engine, install Anaconda and run Jupyter Notebook [from DataCamp](https://www.datacamp.com/community/tutorials/google-cloud-data-science).

---

Among the services:

- Cloud Dataprep;
- Cloud Datalab;
- Cloud Machine Learning Engine;
- BigQuery a data warehouse solution that holds many fascinating Big Data datasets.

For a deeper understanding of Google Cloud:

![](img/Cloud/hand_on_machine_learning_on_google_cloud_platform.png)

# Create an Account and Project

To create your GCP account with the 12-month [free trial](https://cloud.google.com) and/or [free](https://cloud.google.com/free/).  
Once the account is active, the access page is the [Web console](http://console.cloud.google.com/).
Go to the [Resource Management page](https://console.cloud.google.com/cloud-resource-manager).  
Create a new project.  
Go into the project.  
In the roles section of the IAM page, you can add people with specific roles to your project.

# Create an instance

A Virtual Machine (VM) also called "an instance" is an on-demand server that you activate as needed.  
Go to your [dashboard](https://console.cloud.google.com/home/dashboard).  
In the top left menu select "Compute Engine".  
Click on "VM instances". It may take a moment...  
In the dialog, click on the "Create" button.  
Fill out the fields...  
Name `starling` (or any other name), Region (the rule of thumb is to select the cheapest region closest to you to minimize latency and prices vary significantly by region), Zone, Type (default setup `n1-standard-1` with 3.75 Gb RAM and 1vCPU for an estimated price per month), Disk (default Debian GNU/Linux 9 (stretch) OS with 10 Gb), Firewall (access the VM from the internet by allowing http and https traffic).  
Enable a persistent disk for backup purposes: Click on the "Management, Disks, networking, SSH keys" link. Unselect the "Deletion Rule".  
"Create" button.  
It may take a moment...

Notice the link "Equivalent command line" link below the Create button. This link shows the equivalent command line needed to create the same instance from scratch. This is a truly smart feature that facilitates learning the syntax of [gcloud SDK](https://cloud.google.com/sdk/).

# Google's Cloud Shell

Google's Cloud Shell is a stand alone terminal in your browser from which you can access and manage your resources. You activate the google shell by clicking the `>\_` icon in the upper right part of the console page.  
This terminal runs on a f1-micro Google Compute Engine virtual machine with a Debian operating system and 5Gb storage.  
It is created on a per-user, per-session basis. It persists while your cloud shell session is active and is deleted after 20 minutes of inactivity. Since the associated disk is persistent across sessions, your content (files, configurations, ...) will be available from session to session. The cloud shell instance comes pre-installed with the gcloud SDK and vim.  
The instance underlying the cloud shell is just a convenient way to have a resource management environment and store your configurations on an ephemeral instance.  
The VM instance that you just created, named `starling` in the above example, is the instance where you want to install your data science environment.  
Instead of using the Google Cloud shell, you can also [install the gcloud SDK](https://cloud.google.com/sdk/downloads) on your local machine and manage everything from your local environment.  
Commands:

- List your instances, `gcloud compute instances list`
- Stop the instance (takes a few seconds), `gcloud compute instances stop <instance name>`
- Start the instance (also takes a few seconds), `gcloud compute instances start <instance name>`
- and ssh into the starling instance, `gcloud compute ssh <instance name>`

# Debian packages

These package must be intalled:

- bzip2, which is required to install Mini/Anaconda,
- git, which is always useful to have, and
- libxml2-dev, which is not required at this point but you will often need it when installing further Python libraries.

Run the following commands, which work for both Ubuntu and Debian, in the terminal:

    $ sudo apt-get update
    $ sudo apt-get install bzip2 git libxml2-dev

# Anaconda / Miniconda

Install the lighter [Miniconda distribution](https://conda.io/miniconda.html), run

    $ wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
    $ bash Miniconda3-latest-Linux-x86_64.sh

It may take a moment...  

    $ rm Miniconda3-latest-Linux-x86_64.sh
    $ source ~/.bashrc
    $ conda install scikit-learn pandas jupyter ipython

It may take a moment...  

The commands to install the full Anaconda distribution are very similar. Make sure to check the [download page](https://www.anaconda.com/download/#linux) to get the latest version of the shell script file:

    $ wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
    $ bash Anaconda3-5.0.1-Linux-x86_64.sh
    $ rm Anaconda3-5.0.1-Linux-x86_64.sh
    $ source ~/.bahsrc

To verify that everything is installed properly, check your python version with `python --version` and verify that the right python is called by default with the command `which python`.

# Allowing Web Access

The third and final step is to configure your VM to allow web access to your Jupyter notebooks.  
To do that, you will create a firewall rule via the Google Cloud console.  
Go back to your Instances dashboard and in the top left menu, select "VPC Network > Firewall rules".  
Click on the "CREATE FIREWAL RULE" link and fill out the following values:

- Name: jupyter-rule (you can choose any name)
- Source IP ranges: 0.0.0.0/0
- tags cibles: `starling` (ou another chosen name)
- Specified protocols and ports: tcp:8888
- and leave all the other variables to their default values.

This firewall rule allows all incoming traffic (from all IPs) to hit the port 8888.

Now go back to the VM page (top left menu > Compute Engine > VM instances), click on your VM name.  
Make a note of your VM IP address. This is the IP address that you will use in your browser to access your Jupyter environment.  
Internal IP and External IP...  
Make sure the Firewall rules are checked.

# Jupyter Configuration

In the terminal, run `jupyter notebook --generate-config` to generate the configuration file.  
And `jupyter notebook password` to generate a password.

<!--
600pix4x5!
-->

Now edit the configuration file you just created with `vim .jupyter/jupyter_notebook_config.py` or with `nano .jupyter/jupyter_notebook_config.py` and add the following line at the top of the file:
`c.NotebookApp.ip = '*'`.  
(to switch to edit mode in vim, just type the `i` character). Quit and save with the following sequence `ESC:wq`.  
IMPORTANT! This will allow the notebook to be available for all IP addresses on your VM and not just the http://localhost:8888 URL you may be familiar with when working on your local machine.

# Launch

    $ jupyter-notebook --no-browser --port=8888

In your browser go to the URL: http://<your_VM_IP>:8888/ or click on the link to access your newly operational Jupyter notebook.  
Enter the password.  
You are Jupyter Notebook.

# Power

For running classic sklearn or Deep Learning models, bump up the instance's number of CPUs.

# Up/Download

Download from an instance on gcloud to your local folder ./:

    gcloud compute scp [instance_name]:[path to file on instance] ./

Upload some local file to your instance:

    gcloud compute scp  [local file] . [instance_name]:[path]

# Automate

The trick is to use the full path to the python executable which you can find with `which python`.  
Then the following cron job will run your script every hour, 10 mn past the hour:

    10 * * * * [full_path to python]  [full path to your script] > [some log file]

# iPython

Jupyter notebooks are very convenient for online collaborative work. But you can also run an IPython session from your terminal simply with the `ipython` command. That will open an IPython session which has all the bells and whistles of a Jupyter notebook such as magic commands but without the web interface.

# R

It's easy to set up your VM to be enable R notebooks in your Jupyter console.

# Intermezzo

A few notes on your current setup:

- The IP address you used in your browser is ephemeral. Which means that every time you restart your VM, your notebooks will have a different URL. You can make that IP static by going to: Top left menu > VPC Network > External IP addresses and select "static" in the drop down menu.
- The security of your current setup relies on the strength of the Jupyter notebook password that you defined previously. Anyone on the internet can access your Jupyter environment at the same URL you use (and bots will absolutely try). One powerful but very unsecure core feature of Jupyter notebooks is that you can launch a terminal with sudo access directly from the notebook. This means that anyone accessing your notebook could take control of your VM after cracking your notebook password and potentially run anything that would send your bills through the roof. The first level measures to prevent that from happening includes.
- Making sure your Jupyter password is a strong one.
- Remember to **stop** your VM when you're not working on it.
- You are also currently running the server over http and not https which is not secure enough. [Encrypt](https://letsencrypt.org/) provides free SSL/TLS certificates and is the encryption solution recommended in the [Jupyter documentation](https://jupyter-notebook.readthedocs.io/en/latest/public_server.html#running-a-public-notebook-server).
