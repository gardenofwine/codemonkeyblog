---
layout: post
title: iOSDevUK - day 1
---

This is the first part of my [iOSDevUK](http://www.iosdevuk.com/) summary; these are my own personal impressions of the sessions I've attended, and represent things that were interesting/important for me. If a talk or topics are not mentioned, thats because I was already familiar with them, or thought that it is a topic already blogged about plenty.

# Agile Apps
### by [Amy Kinney](https://twitter.com/amykinney)

[Amy gave a talk](http://www.slideshare.net/kinneyamy/agile-apps-iosdevuk-2015-by-amy-kinney) about how to do 'agile' mainly from the standpoint of a contractor building a mobile application for a client. The main points that caught my attention were:

 - Be careful about managing story acceptance criteria. The client mihgt have a different idea of them than what the agile methodology teaches.
 - Make strict feature/bug definitions. Bugs are on the expance of the developer, features are on the client. Prepare for conflicts on this topic as the project progresses.

# From App to Infrastructure
### By [Marc Weeber](https://nl.linkedin.com/pub/marc-weeber/0/a9a/73)

[Marc described in his talk](https://chris-price-b2rp.squarespace.com/s/MarcWeeber.pdf) how a small side project app became an irreplaceable tool for the company maintaining cycling and walking signs all over Holland. some freelancing tools he mentioned:
- A useful blog: inessential.com
- easybooksapp.com - for accounting
- Talking to business minded friends (Its important to put some focus on the business side, as a freelancer)
- Getting financial resources from Holland's government innovation subsidies.

# Xcode into Knowcode
### By [Helen McManus](https://twitter.com/invisiblepixels)

Helen gave an good talk about some "secret" features in Xcode that I can see being very useful in development of iOS (and mac OS) applications.

- The XCode build process is just a wrapped MAKE file. To view the actual build commands:
	1. build the application in xcode.
	1. Go to the "report navigator"
	1. Choose the "build" item, and then right click any build phase int he main content window, and choose `Copy Transcript for Shown Results`.
![](/assets/iosdevuk1/xcode_build_commands.png)
Paste in a text editor, and you'll see the build command and ENV variables being set:

	```
CompileC /Users/me/Library/Developer/Xcode/DerivedData/iOSDevUK-csuolnphgmnwsmdientirmuiyusl/Build/Intermediates/iOSDevUK.build/Debug-iphonesimulator/iOSDevUK.build/Objects-normal/x86_64/BaseSessionTableViewCell.o iOSDevUK/Classes/Sessions/BaseSessionTableViewCell.m normal x86_64 objective-c com.apple.compilers.llvm.clang.1_0.compiler
    cd /Users/me/Development/projects/iOSDevUK
    export LANG=en_US.US-ASCII
    export PATH="/Applications/Xcode 7 gm.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/usr/bin:/Applications/Xcode 7 gm.app/Contents/Developer/usr/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
    ```

 - In Xcode's project __Build Settings__, the names of the differrent settings displayed are in human readable form. These are __NOT__ the actual flags used to build the projects. To see the actual setting names, with which you can search for answers on google and SO, toggle __Editor__ => __Show Settings Names__ ![](/assets/iosdevuk1/xcode_settings_names.png)

 	for example, the real name of `Additional SDKs` is ` 	ADDITIONAL_SDKS`


 - To see the actual definitions of these settings, toggle __Editor__ => __Show Definitions__. For example, the `Base SDK` settings value is defined by `iphoneos` (but what you usually see is `Latest iOS (iOS x.x)`)

 - Before fiddling with the build settings, it is advised first to duplicating a build configuration (usually the `DEBUG` configuration)
 ![](/assets/iosdevuk1/xcode_duplicating_debug_settings.png)
 After that use the duplicated configuration as a playground, while not ruining a good configuration that you know is working.


 - User defined settings can be added to the `Build Settings` ![](/assets/iosdevuk1/xcode_user_defined_Settings.png)
 If you want to access these settings at runtime, you can create an entry in  your `info.plist` file, and set its value to `${the user settings name}`

 - To view the `Build Settings` in text format, copy and paste them into a text file. You would see all the possible settings, but values for them would only appear if you override the iOS default ones. For example:

 	```
 //:configuration = Debug
SDKROOT = iphoneos
GCC_VERSION =
CODE_SIGN_IDENTITY = iPhone Developer

	 ```

 - Use scheme arguments to override settings in NSUserDefaults (like NSDoubleLocalizedStrings). For example, you can override the runtime language of the app by passing an argument of `-AppleLanguages (fr)`. See this [NSHipser article](http://nshipster.com/launch-arguments-and-environment-variables/) for deatils.

	 You cannot, however, know the complete set of settings you can override through scheme arguments. There is certainly a lot of documentation out there about using arguemnts for core data, setting language, RTL and other localization related stuff, but not much else.

 - You can push compile time c `-D` flags into the xcode build phase by doing the follwoing:
 	1. Add a user settings in your build configuration `MY_SETTING = MY_FLAG`
 	2. Add that user setting in the OTHER_CFLAGS build settings as a varaible `$(MY_SETTING)`

 - To run your application with an exisitng Application Data:
 	1. Download application data (`xcappdata`) from an actual device. Xcode calls this "container", but they are the same thing. From the `Devices` screen in Xcode, select your iOS device and click the "Settings" icon, to reveal the `Download Container` option. ![](/assets/iosdevuk1/xcode_download_app_container.png)
 	1. Add it to your xcode project.
 	1. In the Scheme editor, go to "options", and select the application container in the `Application Data` drop down ![](/assets/iosdevuk1/xocde_schem_app_data.png)
 You should now be able to run your application, and it will already be set with whatever data is in the "container"

 - Add a script to your build phase to update your bundle version, so that you always have an updated build number (good for logging, bug reports).

# Debugging Autolayout

## By [Martin Pilkington](https://twitter.com/pilky)

 Having worked with autolayout quite a bit myself in the past, I still found interesting tips from Martin???

 - Horizontal & Vertical autolayout error messages in the console appear seperately.
  - in iOS9, one can tag views with strings, which later on appear in debug/error messages. This would ease debugging as you won't have to guess which view is it exactly that breaks autolayout.
  - in the debugger console type `po [[UIWindow keyWindow] _autolayoutTrace]` for a schematic printout of the whole view hierarchy, with any ambiguous constraints highlighted (see [this  blog post](http://swiftiostutorials.com/using-private-undocumented-ios-methods-debugging/)

	  ```
	|  UIWindow:0x7fec52127d90
	|   UILayoutContainerView:0x7fec52210180
	|   |   UINavigationTransitionView:0x7fec51f2ba50
	|   |   |   UIViewControllerWrapperView:0x7fec51d20d10
	|   |   |   |   •UITableView:0x7fec5581c800
	|   |   |   |   |   UITableViewWrapperView:0x7fec51f47b60
	|   |   |   |   |   |   UITableViewCell:0x7fec51d50dc0'taxiCell'
	|   |   |   |   |   |   |   UITableViewCellContentView:0x7fec51d51110

	  ```
    - To debug views in a running app, press the `Debug View Hierarchy` option in the console view. You will get a live view of the app which you can 3d rotate and further inspect.
  ![](/assets/iosdevuk1/xcode_debug_view_heirarchy.png)
  - Supposedly, the `[view exerciseAmbiguityInLayout]` is supposed to tweak a view with ambiguous layout. [More info here](http://www.informit.com/articles/article.aspx?p=2151265&seqNum=6)
  - In Instruments, there is a tool called "Cocoa Layout". You can use it to track when constraints are added to views, view the stack trace of each constraint that has been added, and collect other info about them.

# Rapid app development with 3rd party Apps

## [Zoltan Varadi](https://twitter.com/iamZoltanVaradi)

Zoltan shared some of the nifty tools he used to develop his latest apps ([slides available here](http://www.slideshare.net/iamZoltanVaradi/tools-and-practices-for-rapid-application-development)):

 - Xcode plugins:
    - [RRConstraintsPlugin](https://github.com/RolandasRazma/RRConstraintsPlugin) - for Xcode 6.1. Adds some ui cues for constraints in the interface builder (such as constraint priority coloring). I don't know if this plugin works on xcode 7.
    - [SCXcodeSwitchExpander](https://github.com/stefanceriu/SCXcodeSwitchExpander) - autocompletes switch cases in code
    - (IconMaker)[https://github.com/kaphacius/IconMaker] - turn any image into an app icon.
    - [FuzzyAutocomplete](https://github.com/FuzzyAutocomplete/FuzzyAutocompletePlugin) - uses the same algorithm of "open quickly" to autocomplete code.  
 - Cocoapods     
    - [MWPhotoBrowser](https://github.com/mwaterfall/MWPhotoBrowser) - Brings awesome photo browsing into your app
    - [MCSwipeTableViewCell](https://github.com/alikaragoz/MCSwipeTableViewCell) - adds swipe action to table view cells (like in the Mail app)
 - [Fabric](https://get.fabric.io/ios?locale=en-us) is an everything manager for your iOS development. It can manage cocoapods, external libraries, signing certificates, dSYMs... Its a concept I don't fully grasp, and I feel that one would need to use it in order to understand what advantages it can bring.
 - Useful code snippets:
  - Cool code snippet to create a "deep" `NSMutableDictionary` from an `NSDictionary` (see [slide 42](http://www.slideshare.net/iamZoltanVaradi/tools-and-practices-for-rapid-application-development) in the presentation)
  - Casting a `_weak` variable into `_string` inside a block to verify if it still exists in memory ([page 44 in the presentation](http://www.slideshare.net/iamZoltanVaradi/tools-and-practices-for-rapid-application-development))
- Useful tools:
  - [Cocoa Controls](https://www.cocoacontrols.com/) - various UI controls sorted by license, platform, language and rating
  - [ReSign app](http://junecloud.com/software/mac/re-sign-ios-app.html) - take an existing IPA and re-sign it with a different certificate without Xcode.
- Blogs:
  - [iOS Dev Weekly](https://iosdevweekly.com/) by [Dave Verwer](https://twitter.com/daveverwer)


# To be continued
