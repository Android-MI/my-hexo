---
title: Setting ANDROID_HOME enviromental variable on MacOS-X

date: 2017-10-17 13:30:12

urlname: Android-Home-Enviiromental

updated: 2017-10-18 13:32:22

tags:
- Android

categories: 
- 工作
- Android

comments: true
---

> [转自stackoverflow](https://stackoverflow.com/questions/19986214/setting-android-home-enviromental-variable-on-mac-os-x)

#### Where the Android-SDK is installed depends on how you installed it. 
* 1. If you downloaded the SDK through their website and then dragged/dropped the Application to your Applications folder, it's most likely here:
``` /Applications/ADT/sdk (as it is in your case). ```
* 2. If you installed the SDK using Homebrew (brew cask install android-sdk), then it's located here:
``` /usr/local/Caskroom/android-sdk/{YOUR_SDK_VERSION_NUMBER} ```
* 3. If the SDK was installed automatically as part of Android Studio then it's located here:
``` /Users/{YOUR_USER_NAME}/Library/Android/sdk ```

#### Once you know the location, open a terminal window and enter the following (changing out the path to the SDK to be however you installed it):
``` export ANDROID_HOME={YOUR_PATH} ```

#### Once you have this set, you need to add this to the PATH environment variable:
``` export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools ```

#### Lastly apply these changes by re-sourcing .bash_profile:
``` source ~/.bash_profile ```

