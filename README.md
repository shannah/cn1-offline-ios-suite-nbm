#Codename One Offline iOS Build Netbeans Module

This Netbeans module allows you to build your [Codename One](http://www.codenameone.com) applications for iOS locally.  It is intended for development only and not all features of Codename One are currently supported [[See issuetracker for details](https://github.com/shannah/cn1-local-build-tools/issues)].

This module is a wrapper for the [Codename One Local iOS Build Ant Task](https://github.com/shannah/cn1-local-build-tools) to more easily integrate local/offline building into [Codename One](http://www.codenameone.com) Netbeans projects.

###IMPORTANT:

This module is designed to be used **for development builds only**.  It includes modifications to XMLVM to allow generated classes to be more self-contained, and thus optimized for faster compilation (when changes are made).  These changes are experimental and may not work correctly in all cases.  You are advised to use this module only as a tool to speed your development process.

**PLEASE USE THE [Codename One Build Server](http://www.codenameone.com/build-server.html) for all of your production builds, and for anything you wish to distribute for use by other users. **

**ALSO NOTE:*** This project is **not affiliated with Codename One, the company**.  It is a community project maintained by [Steve Hannah](http://sjhannah.com).  Builds produced by this project are **not supported by Codename One**.  

Therefore, if you have questions or issues related to applications you have built using this tool, and you post questions to the Codename One mailing list, Stack Overflow, or any other forum, **please state clearly that the build was produced using this project, and not with the build server**.  You will likely be asked to try building with the build server before asking for support. 

If you find bugs, or have questions relating to this library, please post them to [the issue tracker](https://github.com/shannah/cn1-offline-ios-suite-nbm/issues).

----

##Contents:

1. [Requirements](#requirements)
2. [Features](#features)
3. [License](#license)
4. [Installation](#installation)
5. [Updates](#updates)
6. [Usage](#usage)
7. [Limitations](#limitations)
8. [Troubleshooting](#troubleshooting)
9. [Support](#support)
10. [Where can I find the sources?](#where-can-i-find-the-sources)
11. [Credits](#credits)

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

2. Open Netbeans, and select "Plugins" from the "Tools" menu. <br/><img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/tools-menu.png"/>

3. Click on the "Downloaded" tab in the "Plugins" dialog. <br/><img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/plugins-dialog.png" width="600"/>

4. Click the "Add Plugins..." button.  This should open a file dialog.

5. Navigate to and select the `ca-weblite-codename1-netbeans.nbm` file that you downloaded in step 1. <br/> <img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/file-dialog.png" width="400"/>

6. Follow the prompts to complete the installation.

##Updates

Updates are managed through the Netbeans update center.  You should be notified when updates are available and can opt to download them have have them installed automatically.

##Usage

###Building A Codename One Application for iOS Locally

1. Open your Codename One application project in Netbeans.
2. Right click on the project node in the project explorer.  This should reveal the project's contextual menu, and you should see an option called "Build for iOS Locally".<br/> <img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/project-menu.png"/>

If a dialog appears asking you if you want to generate a new Xcode project, just select "OK".  At this point you should see a bunch of output to the "Output" window in Netbeans showing your the progress while it converts your Java files into C files.  If this is your first build, then this part may take 2 or 3 minutes to complete.  If this is a subsequent build then it may take as little as 10 seconds.

After all of the Java files have been converted to C-Sources, Netbeans will automatically open a project in Xcode that contains your project files.

<img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/xcode-project-page.png"/ width="800"/>

At this point you should be able to just build the project in Xcode by selecting "Project" > "Run" or by clicking the "Run" button on the toolbar.

**NOTE:** If this is a "clean" build or it is the first time you have built this project locally, the project may fail to build because the compiler isn't set correctly in project settings.  If this is the case, then you just need to select the "Default Compiler" option for the "Compiler for C/C++/Objective-C" line in your Xcode project's Build settings.  
You can do this by clicking on your Project in the left column, then Clicking on the "Build Settings" tab.

<img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/xcode-project-settings.png"/ width="800"/>

If this is the the first build in your Xcode project, or this is the first build since your last "clean" build, then compilation will take a while (there will be a couple thousand C-source files to compile).  Subsequent compiles will be much faster though (usually a couple of seconds).

If the compile was successful, your app should open in the iOS simulator and should be usable:

<img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/ios-simulator-screenshot.png"/ width="800"/>

Note: This screenshot shows an app opened in the iOS simulator, but you can produce builds for your device also.

##Limitations

1. This module builds apps that are optimized for development. It includes a modified version of XMLVM that disables constant pools and vtable optimizations to make class files more independent and help with making compilation (rather re-compilation) faster.  For this reason (and because these changes are experimental) it is recommended that you only use this module for producing development builds.  Production builds should be generated on the Codename One build server.
2. This module is mostly a wrapper for the [cn1-local-ios-build-tools project](https://github.com/shannah/cn1-local-build-tools).  Therefore you can see a list of features that are not supported in its [issue tracker](https://github.com/shannah/cn1-local-build-tools/issues).

##Troubleshooting

###Xcode Build Fails: Incompatible Compiler

If this is a "clean" build or it is the first time you have built this project locally, the project may fail to build because the compiler isn't set correctly in project settings.  If this is the case, then you just need to select the "Default Compiler" option for the "Compiler for C/C++/Objective-C" line in your Xcode project's Build settings.  
You can do this by clicking on your Project in the left column, then Clicking on the "Build Settings" tab.

<img src="https://raw.github.com/shannah/cn1-offline-ios-suite-nbm/master/screenshots/xcode-project-settings.png"/ width="800"/>

##Support

1. If you are having difficulty with applications that you build using this module, please try to perform the build using the Codename One build server before asking for support.  This module is not supported by the Codename One folks, it is purely a community-driven project.
2. If you are having issues that occur with builds produce by this module, which do not occur when building using the build server, please report them to [the issue tracker](https://github.com/shannah/cn1-offline-ios-suite-nbm/issues).

##Where Can I Find the Sources

This module bundles together code from several different locations:

1. **Codename One Sources** - You can get them from the [Codename One SVN Repository](https://code.google.com/p/codenameone/source/checkout)
2. **XMLVM Sources** - This module uses a modified version of XMLVM.  You can find the sources [here](https://github.com/shannah/cn1/tree/master/Ports/iOSPort/xmlvm).
3. **Codename One Offline iOS Ant Task** - Most of the building functionality of this module is provided by [this ANT task](https://github.com/shannah/cn1-local-build-tools)
4. **Netbeans Module Code** - The actual code for this netbeans module can be found in [this GitHub repository](https://github.com/shannah/cn1-ios-local-builds-nbm)



##Credits


1. Thanks to **Shai Almog** and **Chen Fishbein** of Codename One for developing and maintaining [Codename One](http://www.codenameone.com), a powerful, cross-platform, mobile application toolkit and framework.
2. Thanks for **Arno Puder** and the XMLVM team for developing and maintaining [XMLVM](http://xmlvm.org), a rich and wonderful tool for translating between different programming languages - in this case for the Java to C translator.
3. This project is maintained by **[Steve Hannah](http://sjhannah.com)**.




