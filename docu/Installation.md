# Installation and setup

## Install python package "dhelp"
This package is used by generator to check if ros packages required by
a system (used in *.rossystem) are released. If it is not, it will add
it into "*.repos" if there is Git repository defined in "*.ros2" model,
such as this example: [my_awesome_pkg](https://github.com/ipa320/RosTooling.github.io/blob/main/docu/RosModelDescription.md?plain=1#L63)

1. Clone [ipa-rwu/dhelp](https://github.com/ipa-rwu/dhelp)
    ```
    git clone git@github.com:ipa-rwu/dhelp.git
    # git clone https://github.com/ipa-rwu/dhelp.git
    ```
2. Enter "dhelp" folder, run:
    ```
    ./install.sh
    ```
    It will create a folder named as "venv". It is a virtual environment on top of an existing Python installation. "dhelp" will be installed here.
3. Get the full path of "venv/bin", then run:
   ```
   echo 'export PATH="the full path of venv/bin":$PATH' >> ~/.bashrc
   # e.g.
   # echo 'export PATH=/home/john/deployment_ws/dhelp/venv/bin:$PATH' >> ~/.bashrc
   ```
   ```
   source ~/.bashrc
   ```
### Option 1: Using the Release version (Recommended)

First, the Java environment has to be set. For Linux it can be installed with the following command:

```
sudo apt-get install openjdk-21-jre
```

Then Eclipse can be installed. Please download the installer from the official Eclipse 2024-09 [website](https://www.eclipse.org/downloads/packages/release/2024-09/r). After unpacking the downloaded file, the installer can be run by calling the command _./eclipse-inst_ from the console.

Once you start the installer, select the package "Eclipse Modeling Tools". You can find it just by scrolling or using the searching tool:

![alt text](images/install_eclipse_modeling.png)

Press next, and then pick the Java version 21 and the folder where you would like to install Eclipse.

![alt text](images/install_eclipse_jdk_version.png)

Continue the installation, accepting the license, as usual.

Once the installation is completed, go to _Help_ > _Install New Software..._. To install the latest version of the Deployment tooling, add the update site URL [https://raw.githubusercontent.com/ipa-rwu/deployment-tooling-update-site/refs/heads/main/site.xml](https://raw.githubusercontent.com/ipa-rwu/deployment-tooling-update-site/refs/heads/main/site.xml) in the _Work with_ section.

![alt text](images/install_updatesite.png)
![alt text](images/install_list_packages.png)

If no package is listed, please uncheck the option _Group items by category_. The category _Deployment Tooling Feature_ and _Ros Feature_ (if you didn't install it before) appears in the _Name_ area. Check the box in front of _Deployment Tooling Feature_ and _Ros Feature_, and click _Next_ to review the list of items to be installed. Click _Next_ again to read and accept the terms of the license agreements and afterwards click _Finish_. Eclipse will then start to install the Deployment tooling and its dependencies. If you get a security warning about the authenticity, click OK. Finally, when asked, restart Eclipse to complete the installation process.

### Option 2: Using the source code (for tooling developers)
TODO

## Start the tooling
1. Enter the folder where you install the eclipse from the terminal
2. Check environment variable `PATH`
    ```
    echo $PATH
    ```
    It should include the full path of venv/bin" that you set in [Install python package "dhelp"](#install-python-package-dhelp)
3. Start eclipse
    ```
    ./eclipse
    ```
4. Continue [Set up the tooling environment in eclipse
](Environment_setup.md)
