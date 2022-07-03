---
layout: post
title:  "How to work with Expo Bare Workflow"
date:   2022-06-26 14:34:25
categories: Expo
tags: featured
image: /assets/article_images/2022-06-26-expo-react-native-series/expo-react-native-series-header.jpg
---

We will go through how to run and debug Androd and iOS on an Expo Bare Workflow locally, with Expo Go, and with EAS Build.

This blog assumes you have already installed the usual things you need to run expo apps which is expo-cli, yarn, and node.js

**Note** node version *lts/gallium* worked best for me.

## First Things First...
If you want to run your custom code (custom iOS/Android code) locally, you need to make sure your environment is set up for it. To determine this, you can run
{% highlight shell %}
npx @react-native-community/cli doctor
{% endhighlight %}

For more information on how this command works, check [this blog out](https://reactnative.dev/blog/2019/11/18/react-native-doctor)

The doctor should automatically fix environment issues for you and install whatever it needs to install, but in the event it doesn't, You can install each manually yourself.

### Android
- JDK: version 11.0.14.1 or 11.0.15 worked best for me
- Android Studio: Required for building and installing your app on Android
- Android SDK and Android Emulator: All can be installed in Android Studio
- ANDROID_HOME: environment variables

I won't go through the specifics on how to install each because each one is very google-able.

### iOS
- XCode: Required for building and installing your app on iOS
- CocoaPods: Required for installing iOS dependencies
- ios-deploy: Required for installing your app on a physical device with the CLI
- Watchman: Used for watching changes in the filesystem when in development mode

For iOS, There's really no way to locally build and run without a Mac. If you don't have one, you can use [MacInCloud](https://www.macincloud.com) which lets you rent Mac.

Cocoapods, Watchman, and ios-deploy can all be installed using brew. 

{% highlight shell %}
brew install ios-deploy
brew install watchman
brew install cocoapods
{% endhighlight %}

You can also install Cocoapods from your default ruby available on MacOS
{% highlight shell %}
sudo gem install cocoapods
{% endhighlight %}
After cli doctor is successful, we can now start running our Expo Bare Workflow app.

## Running Expo Bare Workflow without Expo Go

After you have set up your environment as mentioned above. Inside your folder, you can run these commands
{% highlight shell %}
expo run:ios
expo run:android
{% endhighlight %}
These commands will install dependencies, build your project and deploy them to either a simulator or a physical device depending on whats available. 

If you are coming from a **Managed Workflow**, then it will basically eject iOS/Android when you run these commands. More infomation about these commands in the [Expo Up and Running](https://docs.expo.dev/bare/hello-world/#ios-configuration) docs.

if you take a look at your project folder, you will notice that an **ios/** and/or **android/** folder will be created. You can then open these folders in XCode/Android Studio.

### Running on a Physical Device
You can use the QR Code that will be generated when metro is running after expo run. if you're having problems with that, you can also set it to run on a physical device by connecting your device via USB and running
{% highlight shell %}
expo run:ios -d 'device uuid'
{% endhighlight %}
Replace 'device uuid' with the device uuid that you want to deploy your app to. 

To get your device uuid run this in the terminal.
{% highlight shell %}
xcrun xctrace list devices
{% endhighlight %}
[More info on getting device uuid](https://stackoverflow.com/questions/17237354/how-can-i-find-the-device-uuids-of-all-connected-devices-through-a-command-line)

### Installing Dev Client
[Expo Development Installation](https://docs.expo.dev/development/installation/) documentaion will guide you through how install expo-dev-client onto your project. This will give you some quality of life improvements during development.

## Running Expo Bare Workflow with Expo Go

Despite what this [Expo Documentation](https://docs.expo.dev/bare/using-expo-client/) says, it is possible to run **Expo Bare Workflows** with **Expo Go**. The problem is that it won't build the custom code you wrote in your iOS/Android 💩. What this means is that, Expo Go would still work, but it would just ignore your custom code. You can read more about why they did this here [Using Expo Go With Bare Workflow](https://docs.expo.dev/bare/using-expo-client/).

TLDR; If you're app isn't too reliant on custom native code, and you just something quick and easy for your shareholders to run, you can still use Expo Go.

## Running Expo Bare Workflow with EAS Build
If you do need to build your projects without having to configure your machine for it locally, you can always use [EAS Build](https://docs.expo.dev/build/introduction/). What EAS Build allows you to do is to build your Bare Workflow on Expo Servers instead of your machine. This allows Windows machines to create builds for iOS.

The Expo Documentation does a good job in going through how to work with EAS Builds step by step, so I'll just list the docs I've used to make it work here.

- [Configure your project for EAS Build](https://docs.expo.dev/build/setup/) - Will guide you on how to get EAS Build to work on your project

- [Creating and Installing your development build](https://docs.expo.dev/development/getting-started/#creating-and-installing-your-first-development-build) - Will guide you on how to build and run your EAS build to devices/simulators
- [Configuring EAS Build for internal distribution](https://docs.expo.dev/build/internal-distribution/)

**NOTE** I actually also installed expo-dev-client before configuring EAS Build. So yea, try each one and tell me about it. Check out the **Installing Dev Client** section above.

## Closing Thoughts

So this is all I know so far through my journey on Mobile Development using React Native, Expo, and iOS/Android Native code. Feel free to DM me or email me if you have any questions!

I'm also thinking of doing more blogs on different things I couldn't find any blogs for. For fun and for 💰.
> Written with [StackEdit](https://stackedit.io/).