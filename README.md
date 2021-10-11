# React Native Setup For MacBook M1 Chip

React Native Setup On MacBook M1 Natively. No Rosetta Needed.
At the time of writing this blog, I'm running React Native natively without any issues on MacBook with M1 chip.

I've divided this documentation into **two parts**. **First** part only needs to be reproduced once. Meaning that you'll only have to follow the steps once. The **second** part needs to be reproduced every time you want to setup a new project with React Native.


# Follow steps to reproduce

## Part One (One-time setup)

For all the steps if you have previously installed any of the following using Rosetta terminal, kindly uninstall it and reinstall using the following instructions.
We'll be using normal M1 terminal for installing everything.

You need to ensure that you have the following installed.

- **Xcode**
- **Android Studio**
- **adb**
- **Java SDK 8**


I'm using
> React Native version: `0.66.0`
![RN version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Frn-version.png?alt=media&token=4c4f3422-a629-4715-9805-6123ae011fac)

> Xcode version: 13.0
![Xcode version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fxcode-version.png?alt=media&token=71b8f56f-cf09-41e9-9552-42437b3c1ede)


> Android Studio version: `Android Studio Arctic Fox | 2020.3.1 Patch 1`
![android-Studio version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fandroid-studio-version.png?alt=media&token=31e1a9aa-0001-414d-98a5-c91d836cf4ed)

Now Open your terminal and install brew natively

**1- Install latest version of brew**

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

or install it from their **[official website](https://brew.sh/)**

My brew version
![brew version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fbrew-version.png?alt=media&token=e653ca00-df87-4564-8e01-aefe4f174acf
)

**2- Install and update Ruby to latest version**

    brew install ruby

My ruby version
![ruby version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fruby-version.png?alt=media&token=aff71b94-b5c2-462a-8c9d-acc0b5f7c88b)

**3- Install cocoapods using gem**

    sudo gem install cocoapods

My pod version
![pod version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fpod-version.png?alt=media&token=8263935d-8c85-4f1d-a7ec-a72d6e5a6eb4)


**4- Install ffi using gem**

    sudo gem install ffi

**5- Install watchman**

    brew install watchman

My watchman version
![watchman version](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fwatchman-version.png?alt=media&token=89316da7-148d-4819-8810-a6f49e3d3717)

Now that the basic tools are all setup, lets now do some tweaking to make React Native compatible with M1 chip.

Open **Android studio**, then go to `preferences/appearance & Behavior/System Settings/Android SDK`

> Under **SDK Platforms** make sure you have latest android-sdk installed as well as android-sdk 10.0 (Q) installed

![android sdk](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fandroid-sdk.png?alt=media&token=9daa56c3-b33a-43a7-9a9a-a6c5f0a42bba)


> Under **SDK Tools** make sure you have latest Android build tools installed as well as command line tools installed

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fsdk-tools.png?alt=media&token=26a9fefd-5ff1-4119-b9bd-1aa64acd3475
)

> Check mark **show package details** Under **SDK Platforms** and make sure you have latest Android build tools, command line tools installed as well as arm based images of the selected tools installed

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fsdk-platform-packages.png?alt=media&token=5841c913-93fb-4315-91b8-c5b16dbfe9f4)

> Check mark **show package details** Under **SDK Tools** and make sure you have latest Android build tools installed

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fsdk-tools-packages.png?alt=media&token=b226e453-1f9d-41d7-b731-fa063180718d)


> Now go to updates section and make sure you have no updates remaining. 

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fupdates.png?alt=media&token=b5a7ac08-e799-41a2-80fc-a550442421bb)


If you have updates to install, then install them. If for some reason you get update error or compatibility issue while updating. Then go to [official website](https://developer.android.com/studio) of android studio and download the latest version from there. Unpack it and move it to applications folder to replace it with the current version of android studio. This will make sure you have no updates remaining.


🎉🥳 **Congratulations. Part One Done ✅.** if you have successfully come this far then you're almost done. The above steps are to be only produced once and you won't need to apply these steps for future build of react native in your machine 🎉🥳

-------------------------------><-------------------------------------

## Part Two (Follow every time for setup)

Initiate React Native project

    npx react-native init hello --template react-native-template-typescript

Open your project in your code editor and open terminal


Run server by either

    npm run start

Or

    yarn start

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fstart.png?alt=media&token=a7ce99ca-f81f-43c6-a060-71181f67ddf8)


## IOS Setup

open another terminal

run

    npm run ios

Or

    yarn ios

This should pop a IOS device for your and build the react native app on it successfully.
![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fios-success-terminal.png?alt=media&token=12292cbe-902b-4694-b367-8b8f19f90c0e)

if for some reason you get error, then open project [projectname].xcworkspace file in IOS folder using Xcode. Select your IOS device, then clean your project and run the application from Xcode.
This should do the job.
![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fios-success-xcode.png?alt=media&token=940dbf71-a5be-4e03-98ba-a8561672c36b)

**Note**: when installing pods, if `pod install` command fails then use `npx pod-install` for installing pods

## ANDROID Setup

For Android we need to give path to adb once so that after that we are able to run application from terminal directly. for this open the Android folder of the project using **Android Studio**.

**Go to** `preferences/Build, Execution, Deployment/Build Tools/Gradle`

Select **android sdk 11** for use. If it's not installed, then install it.
![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fandroid-sdk-11.png?alt=media&token=38aa74fb-b356-4ae7-8a03-a2eaa4db7c81)

Then if Android Studio shows notification that says **Android Gradle Plugin can be upgraded**? You should upgrade it.

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fgradle-upgrade.png?alt=media&token=3a422e57-9d82-4114-bebc-c7faea916e2e)


After upgradation is done, run project from the Android Studio to give adb a path to the project. This step is needed only once.
This would probably show an error in the emulator which is good and the expected outcome.
![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fandroid-error.png?alt=media&token=57755646-2f13-41f8-a1f7-20dde35873b6)

Now close the Android Studio but keep the emulator running.
Open the project using terminal and 

run

    npm run android

Or

    yarn android


This will build the Android part of your React Native application successfully.

![sdk tools](https://firebasestorage.googleapis.com/v0/b/myfirebase-301718.appspot.com/o/github%2Freact-native-m1-setup%2Fandroid-success.png?alt=media&token=76889b4b-cf0e-483d-bc01-c12666cf9f3e)


🎉 **That's all** 🎉

### some key notes

- First part of the documentation needs to be followed only once

- Second part of the documentation needs to be followed every time you initiate a new project.

- you need to only build project to give adb a path through android studio once

- you just need to open **android emulator** manually if not already opened to run `npx react-native run-android` command successfully.

## Credits

© [Waleed Tariq](https://github.com/Waleed065)
