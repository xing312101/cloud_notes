# Install
> for Windows offline

## Environment Variable (example)

#### ANDROID_HOME:
```
C:\Android
```

#### ANDROID_SDK_ROOT:
```
C:\Android\sdk\Android
```

#### PATH:
```
C:\dart-sdk\bin
C:\flutter\bin
```

## SDK
### Android SDK
#### method 1
> https://developer.android.com/studio/command-line/sdkmanager

```
https://developer.android.com/studio#downloads

using command line tool to get sdkmanager
```


#### method 2
Download from Android Studio or another IDE

### Dart SDK
> https://dart.dev/tools/sdk/archive

### Flutter SDK
> https://flutter.dev/docs/development/tools/sdk/releases?tab=windows


## Android Studio
> https://developer.android.com/studio

### plugins
Need to check the version of plugins and android studio

#### Dart
> https://plugins.jetbrains.com/plugin/6351-dart

#### Flutter
> https://plugins.jetbrains.com/plugin/9212-flutter

## Gradle
> https://gradle.org/releases/

> offline files of Gradle  are copied from another computer which has build apk success.

```
Offline
# gradle-wrapper.properties
## flutter project: android\gradle\wrapper\gradle-wrapper.properties
distributionUrl=file:///c:/x/install/gradle-4.10.2-all.zip

# .gradle directory
## defulat path C:\Users\{{Administrator}}\.gradle
copy file to this path

## environment name
GRADLE_USER_HOME


```

## Intel Hardware Accelerated Execution Manager (HAXM)
> https://github.com/intel/haxm




