---
layout: post
title: DroidConTLV Impressions - part 2
---

This is the last and second part of the [DroidConTLV](http://il.droidcon.com/2015/) summary, and I'm writing it a month after the actual conference took place, out of notes I wrote in real time. These are my own personal impressions of the sessions I've attended, and represent things that were interesting/important for me. I did not mention topics and material of which I am familiar with.

# Deep Linking
### by [Naor Rosenberg](https://www.in.com/in/naorrosenberg)
[Slides](http://www.slideshare.net/DroidConTLV/deeplinking-101-naor-rosenberg-quixey)

The only note I had about this talk is about [Hipmunk](https://www.hipmunk.com/), a Kayak-like website for finding cheap flights and hotels. For some reason this appeared in my notes, and I think Naor mentioned the application as an example of good deep linking, though I'm not sure.

# Wunderlist  
### by [Cesar Valiente](https://twitter.com/cesarvaliente)

Cesar was talking about some hardships that the engineering team at [Wunderlist](https://www.wunderlist.com/) encountered during development.
1. Good truthes were given in the talk, but nothing innovative. He did emphesize the importance of decoupling layers of an application - for instance decouple logic layer from network layer.
1. Websockets - A thorough walkthrough of WS implementations for Android:
  - [Java-Websockets](https://github.com/TooTallNate/Java-WebSocket) - Cesar mentioned there is a problem with SSL in this specific implementation.
  - [Netty](http://netty.io/) - a full fledged communication framework with WebSocket implementation
  - [OKHttp-ws](https://github.com/square/okhttp/tree/master/okhttp-ws) - a new (May 2105) Java library just for Websockets
1. [EventBus](https://github.com/greenrobot/EventBus) - Notification library for Android, used for ineer-process communication.


# Man in the Binder
### by [Michael Shalyt](https://twitter.com/mshalyt) & [Idan Revivo](https://twitter.com/idanr86)

The speakers here put great emphasis on one truth:  "Everything goes through the Binder". The Android [Binder](http://developer.android.com/reference/android/os/Binder.html). Each keyboard keystroke goes through it, any communication an application has with another application on the Android device. As such, a compromised Binder makes your application compromised as well.

# Whats new in Android
### by [Wojtek Kaliciński](https://plus.google.com/+WojtekKalicinski/posts)

There are many article about the new features of Android M. Here are tids and bits that got my attention:
1. Permissions - Accessing information when the user has revoked permission __wont__ result in an exception. Instead, blank info will be returned. For example - asking for the list of user contacts when the user hasn't granted the permission will result in an empty list.
1. [InstanceID](https://developers.google.com/instance-id/) - A unique Id per app installation, across user's devices. If a user has 2 Android devices and is logged into your app on both with the same user - you would be able to distinguish the two by the InstanceID.
1. Google Cloud Messaging (GCM) [Topic Messaging](https://developers.google.com/cloud-messaging/topic-messaging)
 - Its like PubSub for push notifications.


# Reducing APK size
### by [Rotem Mizrachi](https://twitter.com/rotemmiz)

[Joey Simhon](https://twitter.com/joeysim) published a [blog post](http://geeks.everything.me/2015/06/10/taking-the-ks-off-your-apks-part-1/) about his talk in his company's blog website. He is listed in DroidCon's brochure as the speaker, but Rotem replaced him. I recommend reading the whole thing, its pretty interesting.

1. Create different APK's for different devices - There's [Google documentation](http://developer.android.com/training/multiple-apks/screensize.html), but I suggest you read the blog post.
1. [Proguard](http://developer.android.com/tools/help/proguard.html) - enough said
1. [PNGQuant](https://pngquant.org/) - reduce PNG image sizes. Image quality is almost unnoticeable.

Other cool tools mentioned in the talk, but not related directly to APKs:

1. [logcat color](https://github.com/marshall/logcat-color) - a script to colorize the adb logcat output to the console.
1. ReCat - This is an inner tool developed by [Everything.me](http://everything.me/), and __promised__ to be open sourced soon; ReCat is a de-obfuscarot to logcat, much like javascript sourcemaps for chrome devtools.
1. [Realm](https://realm.io/news/realm-for-android/) - Fast DB for Android implemented in C++

# Hacking Apps
### by [Erez Metula](https://twitter.com/erezmetula)
Erez talked about how hackers might exploit the holes in your app's security. Other than mention common culprits in apps, such as poor server side control, Erez advocates the use of his company's security testing platform, [AppUse](https://appsec-labs.com/appuse/). His slides are posted [here](http://www.slideshare.net/DroidConTLV/android-app-hacking-erez-metula-appsec)

Other security tips:
1. Test your app's network communication  with [BurpSuit](https://support.portswigger.net/customer/portal/articles/1841101-configuring-an-android-device-to-work-with-burp)
1. Data storage - SD cards are INSECURE. Be aware of file permissions on internal storage as well.
1. Beware of [Unintended Data Leakage](http://resources.infosecinstitute.com/android-hacking-security-part-4-exploiting-unintended-data-leakage-side-channel-data-leakage/)
1. Use proper encryption - otherwise you might be using Encraption
1. No binary protection - exposes you app for APK analysis, and business logic might leak.

# Magneto, UI Testing
### by [Ran Ben Aharon](http://ranbena.com/)

Ran, also from [Everything.me](http://everything.me/) is an expert on UI Testing on Android, and gave good pointer and ideas for those wanting to test their Android apps. He did promote the use of [Magneto](https://github.com/EverythingMe/magneto), an open source testing tool built at Everything.me, but it wasn't a sales talk.
[Slides about the same topic are available](http://www.slideshare.net/ranbena/magneto-command-your-droids), though they are NOT the slides from DroidCon.

1. [MonkeyTalk](https://www.cloudmonkeymobile.com/monkeytalk) - A full suit UI testing for all mobile platforms. It runs as an eclipse IDE plugin (also works on [Android Studio](https://prativas.wordpress.com/2014/08/15/using-monkeytalk-in-androidstudio/)).
1. [Robotium](https://code.google.com/p/robotium/) & [Espresso](https://code.google.com/p/android-test-kit/wiki/Espresso) - 2 UI testing libs for Android.
1. [Selendroid](http://selendroid.io/) - Like Selenium, but for Android. Compares to [Appium](http://appium.io/).
1. Eliminate time sleeps in Unit Testing.
1. Use `adb` to set the current time & date on your testing device.
1. In the future, Magneto is going to add the ability to fail on GC - an interesting feature for performance critical apps.
1. Join the [Mobile Automators](http://mobileautomators.com/) meetup group in Israel!

# Watson
### by [Ronen Siman Tov](https://twitter.com/simantovronen)
Ronen came to promote the usage of [Watson](http://www.ibm.com/smarterplanet/us/en/ibmwatson/); think AI as a Service. Watson can to linguistic and language analysis on the cloud for you. This talk wasn't Android related at all, but it was intereting to hear about the service.

# Mirror
### by [Yossi Elkrief](https://twitter.com/elkriefy)

Yossi talked about [Mirror](http://jimulabs.com/), a tool that visualizes your Android layouts in real time without compiling your app. If you are developing UI in your application using layout xml files, get yourself familiarized with Mirror. They even have a 30 day trial (that can be extended to 30 more days if you email them).

As a Mirror occasional user (I'm on the extended trial), I find it is somewhat useful when building UI elements, but I have trouble having it display `merge` elements correctly. Also, it slows down Android Studio, which is annoying.
Some new interesting features I've leant about Mirror
1. View animations
1. Add mock data to listviews
1. Hotswap code using [Kotlin](http://kotlinlang.org/) and Mirror - http://jimulabs.com/2015/02/mirror-kotlin/
