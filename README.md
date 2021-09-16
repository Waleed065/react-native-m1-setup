# React Native Setup For Macbook M1 Chip

React Native Setup On Macbook M1 Natively. No Rotteta Needed.

## Follow steps to reproduce

Make sure you have node installed as well as the Android Studio and Xcode are installed to their latest version.
If any of the **brew**, **cocoapods**, **ruby**, **ffi** and **ethon** packages is previously installed using rosetta 2, then uninstall them completely and follow along.

Install brew

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

or install it from their **[official website](https://brew.sh/)**

Install and update Ruby to lastest version

    brew install ruby

Install cocoapods using gem

    sudo gem install cocoapods

Install ffi using gem

    sudo gem install ffi

Install ethon to latest version using gem

    sudo gem install ethon

Install watchman

    brew install watchman

Now that the basic tools are all setup, lets now initiate a new react native project

Initiate react native project

    npx react-native init RnTemplate --template react-native-template-typescript

## IOS Setup

Follow any of the two steps

### 1. Recommended, copy post below script in ios/PodFile

- replace inplace of post_install script

      // ...
      post_install do |installer|
        react_native_post_install(installer)

        # Apple Silicon builds require a library path tweak for Swift library discovery or "symbol not found" for swift things

        installer.aggregate_targets.each do |aggregate_target|
          aggregate_target.user_project.native_targets.each do |target|
            target.build_configurations.each do |config|
              config.build_settings['LIBRARY_SEARCH_PATHS'] = ['$(SDKROOT)/usr/lib/swift', '$(inherited)']
            end
          end
          aggregate_target.user_project.save
        end

        # Flipper requires a crude patch to bump up iOS deployment target, or "error: thread-local storage is not supported for the current target"

        # I'm not aware of any other way to fix this one other than bumping iOS deployment target to match react-native (iOS 11 now)

        installer.pods_project.targets.each do |target|
          target.build_configurations.each do |config|
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '11.0' #it should be 11
          end
        end

        # ...but if you bump iOS deployment target, Flipper barfs again "Time.h:52:17: error: typedef redefinition with different types"

        # We need to make one crude patch to RCT-Folly - set `__IPHONE_10_0` to our iOS target + 1

        `sed -i -e $'s/__IPHONE_10_0/__IPHONE_12_0/' Pods/RCT-Folly/folly/portability/Time.h`
      end
      //...

After that navigate to ios directory and run
pod install

open `[app name].xcworkspace` file in xcode and clean the project with (shift + cmd + k) keys combination.
Now run build command from xcode
remember: On ios react native run via xcode and not via npx

### 2. Else perform these instructions

- open `[app name].xcworkspace` file in xcode create a bridging file

- add **arm64** to build settings devices

- add below command to podFile, under **post_install** script

        //...
        installer.pods_project.build_configurations.each do |config|
        config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "arm64"
        end
        //...

- add below command to ios/{project_name}/AppDelegate.m

        //...
        #import "AppDelegate.h"
        // ADD THIS
        #if RCT_DEV
        #import <React/RCTDevLoadingView.h>
        #endif
        // TILL HERE
        //...
        #endif
        RCTBridge *bridge = [[RCTBridge alloc] initWithDelegate:self launchOptions:launchOptions];
            // ADD THIS
            #if RCT_DEV
              [bridge moduleForClass:[RCTDevLoadingView class]];
        #endif
        RCTRootView *rootView = [[RCTRootView alloc] initWithBridge:bridge
        moduleName:@"appname"
        initialProperties:nil];
        // TILL HERE

-------------------------------><-------------------------------------

## ANDROID Setup

upgrade android studio to latest version which supports m1 machines

1. open android folder of react native project with android studio
2. if android studio promtes to upgrade gradle properties then upgrade them
3. set **java sdk 11** as default
    - **Android Studio** in nav bar of your mac
    - Click **Preferences**
    - Click **Build, Execution, Deployment**
    - Click **Build Tools**
    - Click **Gradle**
    - select **11 version 11..... under Gradle JDK option**. if not found then download it and add it

open your code editor and run
        npx react-native run-android
-------------------------------><-------------------------------------

🎉 **Thats all** 🎉

### release file can be found under

_`~/Library/Developer/Xcode/DerivedData/<app name>/Build/Products/Release-iphoneos/<appname>`_

## License & copyright

© [Waleed Tariq](https://github.com/Waleed065)
