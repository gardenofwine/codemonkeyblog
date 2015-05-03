---
layout: post
---
I was following [the guide to release a cocoapod](http://guides.cocoapods.org/making/making-a-cocoapod.html) on how to publish my pod. One of the steps listed was a linter:

    $ pod lib lint

Sure enough, there were some warnings about my podspec missing adequate description, some dead code in my source, but these were all fixable. However, I also got warning for some of the pods I am dependent on:

```
- WARN  |  SocketRocket/SocketRocket/SRWebSocket.m:1461:32: warning: unused function 'log_queue' [-Wunused-function]
- WARN  | [iOS]  UIImage-ResizeMagick/UIImage+ResizeMagick.m:26:28: warning: implicit conversion loses integer precision: 'long long' to 'NSUInteger' (aka 'unsigned int') [-Wshorten-64-to-32]

[!] BetterContent did not pass validation.
You can use the `--no-clean` option to inspect any issue.
```

*BetterContent is my pod name

Since its not my problem, I didn't take these warning to heart. Until I tried to push my pod to the [trunk](http://guides.cocoapods.org/making/getting-setup-with-trunk):

    $ pod trunk push

And got all the warnings I got with `lint`, plus this error at the end of the console output:

    [!] The podspec does not validate.

Because of these warnings the pod didn't get pushed. I sought the internet for a way to make the warnings of my pod dependencies to go away, with no luck. I even thought of forking these dependencies and fixing the warnings myself, but then I found the solution:

    pod trunk push --allow-warnings

And now you can find [my pod on the trunk](http://cocoapods.org/?q=bettercontent). 
