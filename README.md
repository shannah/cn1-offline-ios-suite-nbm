#Codename One Offline iOS Build Netbeans Module

This Netbeans module allows you to build your [Codename One](http://www.codenameone.com) applications for iOS locally.  It is intended for development only and not all features of Codename One are currently supported.

This module is a wrapper for the [Codename One Local iOS Build Ant Task](https://github.com/shannah/cn1-local-build-tools) to more easily integrate local/offline building into [Codename One](http://www.codenameone.com) Netbeans projects.

###IMPORTANT:

This module is designed to be used **for development builds only**.  It includes modifications to XMLVM to allow generated classes to be more self-contained, and thus optimized for faster compilation (when changes are made).  These changes are experimental and may not work correctly in all cases.  You are advised to use this module only as a tool to speed your development process.

**PLEASE USE THE [Codename One Build Server](http://www.codenameone.com/build-server.html) for all of your production builds, and for anything you wish to distribute for use by other users. **

**ALSO NOTE:*** This project is **not affiliated with Codename One, the company**.  It is a community project maintained by [Steve Hannah](http://sjhannah.com).  Builds produced by this project are **not supported by Codename One**.  

Therefore, if you have questions or issues related to applications you have built using this tool, and you post questions to the Codename One mailing list, Stack Overflow, or any other forum, **please state clearly that the build was produced using this project, and not with the build server**.  You will likely be asked to try building with the build server before asking for support. 

If you find bugs, or have questions relating to this library, please post them to [the issue tracker](https://github.com/shannah/cn1-offline-ios-suite-nbm/issues).

----

##Requirements

* Netbeans 7.4 or higher
* Mac OS X Running Xcode 5
* Java 7
* An existing Codename One Netbeans project

##Features

This module adds three actions to your Codename One project's contextual menu and to the "Build" menu in the menu bar:

1. **Build for iOS Locally** - On first run, it will create an Xcode project with C source files for your application.  This Xcode project can be used to build your project for an iOS device or the iOS simulator.  On subsequent builds, only those classes which have changed since the last build are converted to C-files and copied into the Xcode project.  The initial build will be slow, since it has to generate all of the C-files (expect between 10 and 15 minutes to go from Java source to running App on device or in iOS simulator).  Subsequent builds should be quite fast.  Expect between 10 and 30 seconds depending on how many files were changed.

2. **Clean and Build for iOS Locally** - Deletes any previously generated Xcode project (by this module) and generates it from scratch.  On the initial build this is no different than the *Build for iOS Locally* action.
3. **Open Xcode Project** - Opens the previously generated Xcode project in Xcode. 

##License

* Code in this module is distributed under the Apache License 2.0
* This module also includes Codename One and XMLVM sources, which are distributed under their own licenses.  See [here](http://www.codenameone.com) for information about Codename One's license, and [here](http://www.xmlvm.org) for information about XMLVM's license.

##Installation

1. Download the [Netbeans module](https://s3.amazonaws.com/download.weblite.ca/cn1-offline-ios-nbm/ca-weblite-codename1-netbeans.nbm)
2. Open Netbeans, and select "Plugins" from the "Tools" menu.
 <img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/tools-menu.png"/>
 
3. Click on the "Downloaded" tab in the "Plugins" dialog.
<img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/plugins-dialog.png" width="600"/>

4. Click the "Add Plugins..." button.  This should open a file dialog.
5. Navigate to and select the `ca-weblite-codename1-netbeans.nbm` file that you downloaded in step 1.
<img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/file-dialog.png" width="400"/>

6. Follow the prompts to complete the installation.

##Updates

Updates are managed through the Netbeans update center.  You should be notified when updates are available and can opt to download them have have them installed automatically.

##Usage


