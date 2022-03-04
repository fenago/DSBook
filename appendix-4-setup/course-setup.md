# Appendix 4. Preparing the environmentAppendix 4. Preparing the environment
## A.1 Installing Python and Anaconda
For the projects in this book, we will use Anaconda, a Python distribution that comes with most of the required machine learning packages that you’ll need to use: NumPy, SciPy, Scikit-learn, Pandas, and many more.

### A.1.1 Installing Python and Anaconda on Linux
The instructions in this section will work regardless of whether you’re installing Anaconda on a remote machine or your laptop. Although we tested it only on Ubuntu 18.04 LTS and 20.04 LTS, this process should work fine for most Linux distributions.

#### NOTE
Using Ubuntu Linux is recommended for the examples in this book. It’s not a strict requirement, however, and you should not have problems running the examples in other operating systems. If you don’t have a computer with Ubuntu, it’s possible to rent one online in the cloud. Please refer to the “Renting a server on AWS” section for more detailed instructions.

Almost every Linux distribution comes with a Python interpreter installed, but it’s always a good idea to have a separate installation of Python to avoid trouble with the system Python. Using Anaconda is a great option: it’s installed in the user directory and it doesn’t interfere with the system Python.

To install Anaconda, you first need to download it. Go to https://www.anaconda.com and click Get Starter. Then select Download Anaconda Installer. This should take you to https://www.anaconda.com/products/individual.

Select 64-Bit (x86) installer and the latest available version—3.8 at the moment of writing (figure A.1).

Figure A.1 Downloading the Linux Installer for Anaconda

Next, copy the link to the installation package. In our case it was https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh.

#### NOTENOTE
If a newer version of Anaconda is available, you should install it instead. All the code will work on newer versions without problems.

Now go to the terminal to download it:

1
wget  https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh
copy
Then install it:

1
bash Anaconda3-2021.05-Linux-x86_64.sh
copy
Read the agreement, type “yes” if you accept it, and then select the location where you want to install Anaconda. You can use the default location, but you don’t have to.

During the installation, you’ll be asked if you want to initialize Anaconda. Type “yes,” and it will do everything automatically:

1
2
3
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
[no] >>> yes
copy
If you don’t want to let the installer initialize it, you can do it manually by adding the location with Anaconda’s binaries to the PATH variable. Open the .bashrc file in the home directory and add this line at the end:

1
export PATH=~/anaconda3/bin:$PATH
copy
After the installation has completed, you can delete the installer:

1
rm Anaconda3-2021.05-Linux-x86_64.sh
copy
Next, open a new terminal shell. If you’re using a remote machine, you can simply exit the current session by pressing Ctrl-D and then log in again using the same ssh command as previously.

Now everything should work. You can test that your system picks the right binary by using the which command:

1
which python
copy
If you’re running on an EC2 instance from AWS, you should see something similar to this:

1
/home/ubuntu/anaconda3/bin/python
copy
Of course, the path may be different, but it should be the path to the Anaconda installation.

Now you’re ready to use Python and Anaconda.

### A.1.2 Installing Python and Anaconda on Windows
Linux Subsystem for Windows

The recommended way to install Anaconda on Windows is to use the Linux Subsystem for Windows.

To install Ubuntu on Windows, open the Microsoft Store and look for ubuntu in the search box; then select Ubuntu 18.04 LTS (figure A.2).

Figure A.2 Use Microsoft Store to install Ubuntu on Windows.

To install it, simply click Get in the next window (figure A.3).

Figure A.3 To install Ubuntu 18.04 for Windows, click Get.

Once it’s installed, we can use it by clicking the Launch button (figure A.4).

Figure A.4 Click Launch to run the Ubuntu terminal.

When running it for the first time, it will ask you to specify the username and password (figure A.5). After that, the terminal is ready to use.

Figure A.5 The Ubuntu Terminal running on Windows

Now you can use the Ubuntu Terminal and follow the instructions for Linux to install Anaconda.

## Anaconda Windows Installer

Alternatively, we can use the Windows Installer for Anaconda. First, we need to download it from https://anaconda.com/distribution (figure A.6). Navigate to the Windows Installer section and download the 64-Bit Graphical Installer (or the 32-bit version, if you’re using an older computer).

Figure A.6 Downloading the Windows Installer for Anaconda

Once you’ve downloaded the installer, simply run it and follow the setup guide (figure A.7).

Figure A.7 The installer for Anaconda

It’s pretty straightforward and you should have no problems running it. After the installation is successful, you should be able to run it by choosing Anaconda Navigator from the start menu.

### A.1.3 Installing Python and Anaconda on macOS
The instructions for macOS should be similar to Linux and Windows: select the installer with the latest version of Python and execute it.

## A.2 Running Jupyter
### A.2.1 Running Jupyter on Linux
Once Anaconda is installed, you can run Jupyter. First, you need to create a directory that Jupyter will use for all the notebooks:

1
mkdir notebooks
copy
Then cd to this directory to run Jupyter from there:

1
cd notebooks
copy
It will use this directory for creating notebooks. Now let’s run Jupyter:

1
jupyter notebook
copy
This should be enough if you want to run Jupyter on a local computer. If you want to run it on a remote server, such as an EC2 instance from AWS, you need to add a few extra command-line options:

1
jupyter notebook --ip=0.0.0.0 --no-browser
copy
In this case, you must specify two things:

The IP address Jupyter will use to accept incoming HTTP requests (--ip=0.0.0.0). By default it uses localhost, meaning that it’s possible to access the Notebook service only from within the computer.
The --no-browser parameter, so Jupyter won’t attempt to use the default web browser to open the URL with the notebooks. Of course, there’s no web browser on the remote machine, only a terminal.
NOTE
In the case of EC2 instances on AWS, you will also need to configure the security rules to allow the instance to receive requests on the port 8888. Please refer to the “Renting a server on AWS” section for more details.

When you run this command, you should see something similar to this:

1
2
3
4
5
6
[C 04:50:30.099 NotebookApp] 
   
    To access the notebook, open this file in a browser:
        file:/ / /run/user/1000/jupyter/nbserver-3510-open.html
    Or copy and paste one of these URLs:
        http://(ip-172-31-21-255 or 127.0.0.1):8888/?token=670dfec7558c9a84689e4c3cdbb473e158d3328a40bf6bba
copy
When starting, Jupyter generates a random token. You need this token to access the web page. This is for security purposes, so no one can access the Notebook service but you.

Copy the URL from the terminal, and replace (ip-172-31-21-255 or 127.0.0.1) with the instance URL. You should end up with something like this:

http://ec2-18-217-172-167.us-east-2.compute.amazonaws.com:8888/?token=f04317713e74e65289fe5a43dac43d5bf164c144d05ce613

This URL consists of three parts:

The DNS name of the instance: if you use AWS, you can get it from the AWS console or by using the AWS CLI.
The port (8888, which is the default port for the Jupyter notebooks service).
The token you just copied from the terminal.
After that, you should be able to see the Jupyter Notebooks service and create a new notebook (figure A.8).

Figure A.8 The Jupyter Notebook service. Now you can create a new notebook.

If you’re using a remote machine, when you exit the SSH session the Jupyter Notebook service will stop working. The internal process is attached to the SSH session, and it will be terminated. To avoid this, you can run the service inside screen, a tool for managing multiple virtual terminals:

1
screen -R jupyter
copy
This command will attempt to connect to a screen with the name jupyter, but if no such screen exists, it will create one.

Then, inside the screen, you can type the same command for starting Jupyter Notebook:

1
jupyter notebook --ip=0.0.0.0 --no-browser
copy
Check that it’s working by trying to access it from your web browser. After verifying that it works, you can detach the screen by pressing Ctrl-A followed by D: first press Ctrl-A, wait a bit, and then press D (for macOS, first press Ctrl-A and then press Ctrl-D). Anything running inside the screen is not attached to the current SSH session, so when you detach the screen and exit the session, the Jupyter process will keep running.

You can now disconnect from SSH (by pressing Ctrl-D) and verify that the Jupyter URL is still working.

A.2.2 Running Jupyter on Windows
As with Python and Anaconda, if you use the Linux Subsystem for Windows to install Jupyter, the instructions for Linux should work for Windows too.

By default, there’s no browser configured to run in the Linux Subsystem. So we need to use the following command for launching Jupyter:

1
jupyter notebook --no-browser
copy
Alternatively, we can set the BROWSER variable to point it to a browser from Windows:

1
export BROWSER='/mnt/c/Windows/explorer.exe'
copy
However, if you didn’t use the Linux Subsystem and installed Anaconda using the Windows Installer, starting the Jupyter Notebook service is different.

First, we need to open the Anaconda Navigator in the start menu. Once it’s open, find Jupyter in the Applications tab and click Launch (figure A.9).

Figure A.9 To run the Jupyter Notebook service, find Jupyter in the applications tab and click Launch.

After the service launches successfully, the browser with Jupyter should open automatically (figure A.10).

Figure A.10 The Jupyter Notebook service launched using Anaconda Navigator

### A.2.3 Running Jupyter on MacOS
The instructions for Linux should also work for macOS, with no additional changes.

# A.3 Installing the Kaggle CLI
The Kaggle CLI is the command-line interface for accessing the Kaggle platform, which includes data from Kaggle competitions and Kaggle datasets.

You can install it using pip:

1
pip install kaggle --upgrade
copy
Then you need to configure it. First, you need to get credentials from Kaggle. For that, go to your Kaggle profile (create one if you don’t have one yet), located at https://www.kaggle.com/<username>/account. The URL will be something like https://www.kaggle.com/agrigorev/account.

In the API section, click Create New API Token (figure A.11).

Figure A.11 To generate an API token to use from the Kaggle CLI, click Create New API Token on your Kaggle account page.

This will download a file called kaggle.json, which is a JSON file with two fields: username and key. If you’re configuring the Kaggle CLI on the same computer you used to download the file, you should simply move this file to the location where the Kaggle CLI expects it:

1
2
mkdir ~/.kaggle
mv kaggle.json ~/.kaggle/kaggle.json
copy
If you’re configuring it on a remote machine, such as an EC2 instance, you need to copy the content of this file and paste it into the terminal. Open the file using nano (this will create the file if it doesn’t exist):

1
2
mkdir ~/.kaggle
nano ~/.kaggle/kaggle.json
copy
Paste in the content of the kaggle.json file you downloaded. Save the file by pressing Ctrl-O and exit nano by pressing Ctrl-X.

Now test that it’s working by trying to list the available datasets:

1
kaggle datasets list
copy
You can also test that it can download datasets by trying the dataset from chapter 2:

1
kaggle datasets download -d CooperUnion/cardataset
copy
It should download a file called cardataset.zip.

# A.4 Accessing the source code
We’ve stored the source code for this book on GitHub, a platform for hosting source code. You can see it here: https://ernesto.net.

GitHub uses Git to manage code, so you’ll need a Git client to access the code for this book.

Git comes preinstalled in all the major Linux distributions. For example, the AMI we used for creating an instance with Ubuntu on AWS already has it.

If your distribution doesn’t have Git, it’s easy to install it. For example, for Debian-based distributions (such as Ubuntu), you need to run the following command:

1
sudo apt-get install git
copy
On macOS, to use Git you need to install Command Line Tools or, alternatively, download the installer at https://sourceforge.net/projects/git-osx-installer/.

For Windows, you can download Git at https://git-scm.com/download/win.

Once you have Git installed, you can use it to get the book’s code. To access it, you need to run the following command:

1
git clone https://github.com/alexeygrigorev/mlbookcamp-code.git
copy
Now you can run Jupyter Notebook:

1
2
cd mlbookcamp-code
jupyter notebook
copy
If you don’t have Git and don’t want to install it, it’s also possible to access the code without it. You can download the latest code in a zip archive and unpack it. On Linux, you can do that by executing these commands:

1
2
3
4
wget -O mlbookcamp-code.zip \
    https://github.com/alexeygrigorev/mlbookcamp-code/archive/master.zip  
unzip mlbookcamp-code.zip
rm mlbookcamp-code.zip
copy
You can also just use your web browser: type the URL, download the zip archive, and extract the content.

# A.5 Installing Docker
In chapter 5, we use Docker to package our application in an isolated container. It’s quite easy to install.

## A.5.1 Installing Docker on Linux
These steps are based on the official instructions for Ubuntu from the Docker website (https://docs.docker.com/engine/install/ubuntu/).

First, we need to install all the prerequisites:

1
2
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
copy
Next, we add the repository with the Docker binaries:

1
2
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
copy
Now we can install it:

1
2
sudo apt-get update 
sudo apt-get install docker-ce
copy
Finally, if we want to execute Docker commands without sudo, we need to add our user to the docker user group:

1
sudo adduser $(whoami) docker
copy
Now you’ll need to reboot your system. In the case of EC2 or another remote machine, just logging off and on is enough.

To test that everything works fine, run the hello-world container:

1
docker run hello-world
copy
You should see a message saying that everything works:

1
2
Hello from Docker!
This message shows that your installation appears to be working correctly.
copy
## A.5.2 Installing Docker on Windows
To install Docker on Windows, you need to download the installer from the official website (https://hub.docker.com/editions/community/docker-ce-desktop-windows/) and simply follow the instructions.

## A.5.3 Installing Docker on MacOS
Like with Windows, installing Docker on MacOS is simple: first, download the installer from the official website (https://hub.docker.com/editions/community/docker-ce-desktop-mac/), and then follow the instructions.
