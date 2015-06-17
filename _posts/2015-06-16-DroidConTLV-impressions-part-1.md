---
layout: post
title: DroidConTLV Impressions - part 1
---

On June 10-11 I attended DroidConTLV (Which was actually in a nearby town called Rishon LeZion), and here are my impressions from the sessions I attended.

## Performance Matters - [Ran Nachmany](https://www.linkedin.com/in/rannachmany)

Ran gave a good keynote about performance from the battary life perspective. What are common drainers of the battary, and tips about how to overcome them.



__Facts:__

1. From some survey, 70% of Battary usage goes to analytics, ads and GPS.

<br>

__Tips:__

1. Defer work to when is best for the battary (i.e. When connected to power, or when another app wakes up the device)
2. [WakeLock API](http://developer.android.com/reference/android/os/PowerManager.WakeLock.html) - is dangerous, and can cause power drainage if not used correctly
3. [AlarmManager.setInexact](http://developer.android.com/reference/android/app/AlarmManager.html#setInexactRepeating(int, long, long, android.app.PendingIntent)) - is a wonderful way to give the operating system a chance to optimize power by selecting the best times for application tasks to run. Use this feature if you don't require an exact timing for an operation. 
4. [Passive Location](http://developer.android.com/reference/android/location/LocationManager.html#PASSIVE_PROVIDER) - a way to piggie back on another application's request for location. Your app gets the location without actually initiating a GPS request, thus reducing the battery usage calculated for your app by the system.
5. [JobScheduler](https://developer.android.com/reference/android/app/job/JobScheduler.html) (API 21 and up), [GCMNetworkManager](https://developers.google.com/cloud-messaging/network-manager) - ways to batch expansive network operations on cellular network. 
6. JSON sucks, it uses a lot of space and requires a lot of memory to parse and serialize. Instead, use [FlatBuffer](http://android-developers.blogspot.co.il/2014/06/flatbuffers-memory-efficient.html)
7. Reduce bitmap image sizes by using [RGB-565](http://developer.android.com/reference/android/graphics/Bitmap.Config.html#RGB_565) instead of [ARGB-8888](http://developer.android.com/reference/android/graphics/Bitmap.Config.html#ARGB_8888). Takes 50% of memory, and hardly noticable. 
8. Use [ArrayMap](https://developer.android.com/reference/android/support/v4/util/ArrayMap.html) instead of a `HashMap` for small sized maps. Its more memory efficient.
9. Avoid unintended [AutoBoxing](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html) while using HashMaps. Using an int as the key in a HashMap can cause extrenous computations for the AutoBoxing. Instead, for smaller sized Hashes, use [SparseArray](http://developer.android.com/reference/android/util/SparseArray.html).
10. Enums are Evil! They use much more memory than other solutions. Read this [SO  thread](http://stackoverflow.com/a/25306325/280503) for details

In general, I think Ran would like all the Android developers to read the [memory management guide for Android](https://developer.android.com/training/articles/memory.html).

## Touch Events - [Oren Barad](https://www.linkedin.com/pub/oren-barad/16/986/936)
Oren was deep diving into how touch events propagate through the views when a user taps or swipes. Some of the topics that were interesting to me:

1. [dispatchTouchEvent](http://developer.android.com/reference/android/view/ViewGroup.html#dispatchTouchEvent%28android.view.MotionEvent%29), the first method to be called when there is a touch event
2. [requestDisallowInterceptTouchEvent](http://developer.android.com/reference/android/view/ViewGroup.html#requestDisallowInterceptTouchEvent%28boolean%29), when a child view (mainly inside a scrollview) wants to override their parent handling of the touch event.
3. [GestureDetector](http://developer.android.com/reference/android/view/GestureDetector.html), I didn't know such a class exists for Android. Coming from iOS, this is pretty familiar. 

## 3 Things every Android developer should know - [Ido Volff](https://www.linkedin.com/pub/ido-volff/20/21a/aa2)

This talk had a strong marketing feel to it. Ido was all about how Microsoft is great, and that all Android developers should be aware of that. I don't like these kind of talks too much, because they don't give technical details. There wasn't much in the talk I couldn't have read about online; [project Astoria](https://dev.windows.com/en-us/uwp-bridges/project-astoria) and [Azure Mobile services](http://azure.microsoft.com/en-gb/documentation/services/mobile-services/)

## The "Rounds" project - [Berry Ventura Lev](https://www.linkedin.com/in/berryventura) & [Yohay Barsky](https://www.linkedin.com/pub/yohay-barsky/a/674/aa7)
[Rounds](http://www.rounds.com/) is a video chat application which I haven't heard of until DroidCon. Berry and Yohay came to talk about some of the technical and product details about how Rounds grew:

1. Localization tools - using [POEditor](http://poedit.net/) apparently helped them translate the app to all the languages.
2. Testing - [AppFairy](https://www.testfairy.com/) adds a video and stats to every crash your testers encounter. [Applause](http://www.applause.com/) is kinda like TestFlight for Android.
3. [UniversalImageLoader](https://github.com/nostra13/Android-Universal-Image-Loader) - To attend your Android image loading needs

They also said they are open sourcing some of the tools they developed in-house. Currently, [their github](https://github.com/rounds/rounds-android-goodies/tree/9f3ad33d5f3a78969f5292efba69c3126654d500) lacks documentation, but hopefully they will add it soon.

## Libs - [Royi benyossef](https://www.linkedin.com/in/royiby) ([slides available](http://www.slideshare.net/RoyiBenyossef/with-a-little-help-from-my-libs))

Royi talked about the new support library, and Android development in general.

1. ActionBars are dead. Use [App Bars](http://www.android4devs.com/2014/12/how-to-make-material-design-app.html).
2. [AppCompatDelegate](https://chris.banes.me/2015/04/22/support-libraries-v22-1-0/) - a new way to be backwards compatible. It seemed pretty simple when Royi was talking about it, but now I find I don't quite understand how this is used.
3. Use [RecyclerViews](http://developer.android.com/reference/android/support/v7/widget/RecyclerView.html), not ListViews. Its better when used with a [SortedList](https://developer.android.com/reference/android/support/v7/util/SortedList.html)
4. [Palette.from(Bitmap bitmap)](https://developer.android.com/reference/android/support/v7/graphics/Palette.html#from%28android.graphics.Bitmap%29) - a faster way to extract those solid colors from your bitmap.
5. [AndroidJUnitRunner](http://developer.android.com/reference/android/support/test/runner/AndroidJUnitRunner.html) - allows running JUnit4 style tests with instrumentation support. The old [InstrumentationTestRunner](http://developer.android.com/tools/testing/testing_android.html#InstrumentationTestRunner) Only supports JUnit3 style tests. More info [here](http://stackoverflow.com/a/11916340/280503)
6. [Espresso Test Framework](https://code.google.com/p/android-test-kit/wiki/Espresso) - Much better than appium, since it runs from within the application code. Appium, on the other hand, runs on many platforms, including iOS.
7. [UIAutomator](https://developer.android.com/tools/testing-support-library/index.html#UIAutomator) - Like Espresso, but runs outside the context of the app code. Suited for black box testing.



## To be continued
This post is getting too long, so I'm posting it as "part 1". Hopefully "part 2" will follow soon (and perhaps part 3 as well)