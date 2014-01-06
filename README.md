Ghost Log
=========

Ghost Log is an Android application that displays the device logcat buffer in a system overlay window.

![screenshot](https://raw.github.com/jgilfelt/GhostLog/master/screens.jpg "screenshot")

<a href="https://play.google.com/store/apps/details?id=com.readystatesoftware.ghostlog">
  <img alt="Android app on Google Play"
       src="https://developer.android.com/images/brand/en_app_rgb_wo_60.png" />
</a>

**NOTE: Device root (superuser) access is required to read system logs on Android 4.1 and above.**

Non-root users can still use Ghost Log with their own apps via intent integration - see below.

Features:

* Persistent logcat display as a system overlay
* Customisable log filters and display options
* Auto filter by the current foreground Activity process
* Quick access to pause/play, clear & share functions via rich notification
* Integration support for non-root devices


Non-root Integration
--------------------

Developers can use Ghost Log to display log messages generated by their own apps on non-rooted devices via a broadcast intent interface. This is currently in an experimental phase.

Integration will enable your app to receive messages from the Ghost Log app to start and stop a service inside your app which will monitor and broadcast all log output generated by your application processes back to Ghost Log for display.

**NOTE: You should enable this integration for debug builds only to avoid exposing log output to third parties in production.**

#### Gradle

If you are using the Gradle build system, simply add the following dependency in your `build.gradle` file:

```groovy
dependencies {
    debugCompile 'com.readystatesoftware.ghostlog:ghostlog-integration:+@aar'
}
```

Using `debugCompile` (recommended) ensures the integration library is never compiled into a release build.

#### Ant/Eclipse

If you are using the old build system, download and place the integration library [JAR][1] inside your project `libs` folder and add the following to your `AndroidManifest.xml` (inside the `<application>` tag):

```xml
<!--Receives intents from Ghost Log app to start & stop the integration service-->
<receiver android:name="com.readystatesoftware.ghostlog.integration.IntegrationReceiver" 
    android:permission="com.readystatesoftware.ghostlog.permission.READ_LOGS" >
    <intent-filter>
        <action android:name="com.readystatesoftware.ghostlog.integration.COMMAND" />
    </intent-filter>
</receiver>
<!--Reads logs and broadcasts them to Ghost Log-->
<service android:name="com.readystatesoftware.ghostlog.integration.IntegrationService" />
```

Credits
-------

Author: [Jeff Gilfelt](https://github.com/jgilfelt)

Uses elements from [CatLog](https://github.com/nolanlawson/Catlog) by [Nolan Lawson](https://github.com/nolanlawson)

License
-------

    Copyright (C) 2014 readyState Software Ltd

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

 [1]: http://repository.sonatype.org/service/local/artifact/maven/redirect?r=central-proxy&g=com.readystatesoftware.ghostlog&a=ghostlog-integration&v=LATEST&&c=jar