# react-native-errors-and-solutions

1. First issue:
    (Use `node --trace-warnings ...` to show where the warning was created)
Jetifier found 1274 file(s) to forward-jetify. Using 4 workers...
info JS server already running.
info Installing the app...
Starting a Gradle Daemon, 1 busy and 2 incompatible and 1 stopped Daemons could not be reused, use --status for details
> Task :app:processDebugMainManifest FAILED

Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.

You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.

See https://docs.gradle.org/7.2/userguide/command_line_interface.html#sec:command_line_warnings
81 actionable tasks: 2 executed, 79 up-to-date

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:processDebugMainManifest'.
> Unable to make field private final java.lang.String java.io.File.path accessible: module java.base does not "opens java.io" to unnamed module @f845136

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 48s

error Failed to install the app. Make sure you have the Android development environment set up: https://reactnative.dev/docs/environment-setup.
Error: Command failed: gradlew.bat app:installDebug -PreactNativeDevServerPort=8081

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':app:processDebugMainManifest'.
> Unable to make field private final java.lang.String java.io.File.path accessible: module java.base does not "opens java.io" to unnamed module @f845136

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 48s

    at makeError (C:\Users\solom\srvme_provider\node_modules\execa\index.js:174:9)
    at C:\Users\solom\srvme_provider\node_modules\execa\index.js:278:16
    at processTicksAndRejections (node:internal/process/task_queues:96:5)
    at async runOnAllDevices (C:\Users\solom\srvme_provider\node_modules\@react-native-community\cli-platform-android\build\commands\runAndroid\runOnAllDevices.js:109:5)
    at async Command.handleAction (C:\Users\solom\srvme_provider\node_modules\@react-native-community\cli\build\index.js:192:9)
info Run CLI with --verbose flag for more details.

# Solution
### Add this line 👇 to your gradle.properties in the root file of your android folder
>>>>> org.gradle.jvmargs=-Xmx1536M --add-exports=java.base/sun.nio.ch=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED --add-opens=java.base/java.lang.reflect=ALL-UNNAMED --add-opens=java.base/java.io=ALL-UNNAMED --add-exports=jdk.unsupported/sun.misc=ALL-UNNAMED











##### 2.I use a login in my app, when I test on development environment on my phone I have any trouble I can log in. But when I build the release APK it seems like the app can not connect with the fetch (the code enter in the catch of the fetch)
My AndroidMainfest.xml has the INTERNET pemission. This issue Arises when you use the api link is *http* instead of *https*

#  Solution 
### This line 👇  in your <application> tag in android\app\src\main\AndroidManifest.xml
    >>>>> android:usesCleartextTraffic="true" 
    
    
##### 3.Flat List - ScrollToIndex should be used in conjunction with getItemLayout or onScrollToIndexFailed

# Solution 
Get the flatlist ref by using useRef or ref in class component and use the onScrollToIndexFailed props of the flatlist to handle it
as shown below 👇
>>>> <FlatList
      ref={flatListRef}
      ...
      onScrollToIndexFailed={({
        index,
        averageItemLength,
      }) => {
        // Layout doesn't know the exact location of the requested element.
        // Falling back to calculating the destination manually
        flatListRef.current?.scrollToOffset({
          offset: index * averageItemLength,
          animated: true,
        });
      }}
    />
# Could not find com.facebook.react:react-native:0.68.2.
## Solution 
### Add this fix to your android -> build.gradle file as follows:
    buildscript {
    // ...
    }

    allprojects {
        repositories {
           exclusiveContent {
               filter {
                   includeGroup "com.facebook.react"
               }
               forRepository {
                   maven {
                       url "$rootDir/../node_modules/react-native/android"
                   }
               }
           }
            // ...
        }
    }    
    
