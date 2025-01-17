---
title: Configuring Android
description: Configuring Android
contributors:
  - mlynch
  - jcesarmobile
canonicalUrl: https://capacitorjs.com/docs/android/configuration
---

# Configuring Android

Android apps manage permissions, device features, and other settings by modifying `AndroidManifest.xml`.

This file references values from other files in `res/values/`, to make it easy to update them separately, including `styles.xml` and `strings.xml`.

This article covers the basic modifications you'll need to make to your app. Read the [Android Manifest](https://developer.android.com/guide/topics/manifest/manifest-intro.html) docs to learn a whole lot more.

## Changing App ID

To modify the bundle/app id for your app, edit the `applicationId` line in `android/app/build.gradle`:

```groovy
applicationId "com.getcapacitor.myapp"
```

## Changing App Name

To change the name of your app, change the value for `app_name` in `strings.xml`:

```xml
<string name="app_name">MyApp</string>
```

You probably also want to set the Activity name to match the App, for apps that plan to only have one activity (the main web activity running your app):

```xml
<string name="title_activity_main">MyApp</string>
```

## Deeplinks (aka Android App Links)

> For a complete Deep Links guide, [see here](/guides/deep-links.md).

To enable deeplinking through Android App Links, follow the official Android guide on [Adding Android App Links](https://developer.android.com/studio/write/app-link-indexing). Android Studio comes with a handy wizard for configuring App Links.

Once configured, the [getLaunchUrl in the App API](/apis/app.md#getlaunchurl) will provide any URL the app was launched with, and the [appUrlOpen event](/apis/app.md#addlistener-1) will fire any time the app receives a new App Link deeplink.

## Changing Custom URL

Your app can respond to custom URLs on launch, making it possible to handle deeplinks and app interactions.

To change the URL, search for and modify this line in `strings.xml`. It's recommended to set this to the bundle/app id.

```xml
<string name="custom_url_scheme">com.getcapacitor.myapp</string>
```

In this example, the app will respond to URLs with the `com.getcapacitor.myapp://` scheme.

To get any custom URL the app may have launched with, see the Deeplinks section above this one.

## Setting Permissions

In Android, permissions your app will need are defined in `AndroidManifest.xml` inside of the `<manifest>` tag, generally at the bottom
of the file.

For example, here's what adding Network permissions looks like:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.getcapacitor.myapp">
    <activity>
      <!-- other stuff -->
    </activity>

    <!-- More stuff -->

    <!-- Your permissions -->

    <!-- Network API -->
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
</manifest>
```

Generally, the plugin you choose to use will ask you to set a permission. Add it in this file.

## Default Permissions

By default, the entire initial permissions requested for the latest version of Capacitor with the standard plugins can be found in the android-template's [AndroidManifest.xml](https://github.com/ionic-team/capacitor/blob/2.x/android-template/app/src/main/AndroidManifest.xml)
