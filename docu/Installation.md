# Installation and setup

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
