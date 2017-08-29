# SampleApp
# Android Project Structure


[![Codacy Badge](https://api.codacy.com/project/badge/Grade/2a8eb532d98842f6966bc164a896419a)](https://www.codacy.com/app/saveendhiman/SampleApp?utm_source=github.com&utm_medium=referral&utm_content=saveendhiman/SampleApp&utm_campaign=badger)
[![Twitter](https://img.shields.io/badge/Twitter-@saveendhiman-blue.svg?style=flat)](https://twitter.com/saveendhiman)

[![API](https://img.shields.io/badge/API-14%2B-yellow.svg?style=flat)](https://android-arsenal.com/api?level=14)

[![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)


Hi guys, I have made one Project Structure for Android. This is the open project for any contributer who want to improve something here.

This a Sample Project Structure for Android which you can follow for a clean architecture.

It shows usage of following libraries:

* [Retrofit2] for REST API.

* [RX java] for background process and Retrofit integration.

* [Dagger2] for dependency injection.

* [Firebase] for push notifications.

* [Calligraphy] for font.

* [Picasso] for image loading.

* [Komensky] validations for annotation based validations.

* [Fabric] for crashlytics.

* [Butterknife] for view binding.

* [Timber] for logging.

It uses MVP (Model View Presenter) pattern. MVP is a derivative from the well known MVC (Model View Controller), which for a while now is gaining importance in the development of Android applications.This project also contains basic utility classes required for day to day programming.


Location Handling by fused api.

Utils classes.


# Here is what the app gradle look likes.

    buildscript {
    repositories {
        maven { url 'https://maven.fabric.io/public' }
    }

    dependencies {
        classpath 'io.fabric.tools:gradle:1.24.0'
    }
}
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply plugin: 'kotlin-android-extensions'
apply plugin: 'io.fabric'
apply plugin: 'com.neenbedankt.android-apt'
apply plugin: 'me.tatarka.retrolambda'
apply plugin: 'android-apt'

android {
    signingConfigs {
        configprod {
            keyAlias 'sampleapp'
            keyPassword 'welcome'
            storeFile file('/Users/saveendhiman/Documents/sampleapp/keyhash.jks')
            storePassword 'welcome'
        }
    }

    compileSdkVersion rootProject.ext.compileSdkVersion
    buildToolsVersion rootProject.ext.buildToolsVersion

//app versioning
    def versionMajor = 1
    def versionMinor = 0
    def versionPatch = 0
    def versionBuild = 0

    defaultConfig {
        applicationId "com.sampleapp"
        minSdkVersion rootProject.ext.minSdkVersion
        vectorDrawables.useSupportLibrary = true
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode versionMajor * 10000 + versionMinor * 1000 + versionPatch * 100 + versionBuild
        versionName "${versionMajor}.${versionMinor}.${versionPatch}"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
            debuggable false
            signingConfig signingConfigs.configprod
        }
        debug {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }

    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    lintOptions {
        checkReleaseBuilds false
        abortOnError false
    }
    buildToolsVersion rootProject.ext.buildToolsVersion
}

repositories {
    maven {
        url "https://jitpack.io"
    }
    maven { url 'https://maven.fabric.io/public' }
    mavenCentral()
}

dependencies {

    compile fileTree(include: ['*.jar'], dir: 'libs')
    compile "com.android.support:appcompat-v7:$rootProject.supportLibraryVersion"
    compile "com.android.support:design:$rootProject.supportLibraryVersion"
    apt "com.google.dagger:dagger-compiler:$rootProject.daggerVersion"
    provided "org.glassfish:javax.annotation:$rootProject.ext.annotationVersion"
    compile "com.google.dagger:dagger:$rootProject.daggerVersion"
    compile "com.squareup.retrofit2:retrofit:$rootProject.ext.retrofitVersion"
    compile "com.squareup.retrofit2:converter-gson:$rootProject.ext.retrofitVersion"
    compile "com.squareup.okhttp3:logging-interceptor:$rootProject.ext.loggerVersion"
    compile 'com.squareup.okhttp3:okhttp:3.6.0'
    compile "com.jakewharton:butterknife:$rootProject.ext.butterknifeVersion"
    apt "com.jakewharton:butterknife-compiler:$rootProject.ext.butterknifeVersion"
    compile "com.jakewharton.timber:timber:$rootProject.ext.timberVersion"
    compile "com.google.android.gms:play-services-location:$rootProject.ext.playServiceVersion"
    compile "com.google.android.gms:play-services-places:$rootProject.ext.playServiceVersion"
    compile "com.google.firebase:firebase-messaging:$rootProject.ext.playServiceVersion"
    compile "com.google.android.gms:play-services-maps:$rootProject.ext.playServiceVersion"
    compile "com.google.firebase:firebase-core:$rootProject.ext.playServiceVersion"
    compile "uk.co.chrisjenx:calligraphy:$rootProject.ext.calligraphyVersion"
    compile "com.squareup.picasso:picasso:$rootProject.ext.picassoVersion"
    compile "eu.inmite.android.lib:android-validation-komensky:$rootProject.ext.komenskyValidation@aar"
    compile "com.facebook.android:facebook-android-sdk:$rootProject.ext.facebookVersion"
    compile("com.crashlytics.sdk.android:crashlytics:$rootProject.ext.crashVersion@aar")
            {
                transitive = true;
            }
    compile "io.reactivex.rxjava2:rxandroid:$rootProject.ext.rxAndroidVersion"
    compile "io.reactivex.rxjava2:rxjava:$rootProject.ext.rxJavaVersion"
    compile "com.squareup.retrofit2:adapter-rxjava2:$rootProject.ext.retrofitVersion"
    testCompile "junit:junit:$rootProject.ext.junitVersion"
    compile "com.android.support.constraint:constraint-layout:$rootProject.ext.constraintVersion"
    compile "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    compile "com.android.support:multidex:$rootProject.ext.multidexVersion"
    compile "com.github.d-max:spots-dialog:$rootProject.ext.dialogProgressVersion@aar"
    compile "com.github.bumptech.glide:glide:$rootProject.ext.glideVersion"
    compile "com.firebase:firebase-jobdispatcher-with-gcm-dep:$rootProject.ext.jobdispatcherVersion"
    compile "com.airbnb.android:lottie:$rootProject.ext.lottieVersion"

}
apply plugin: 'com.google.gms.google-services'

    
##DONATIONS

This project needs you! If you would like to support this project's further development, the creator of this project or the continuous maintenance of this project, feel free to donate. Your donation is highly appreciated (and I love food, coffee and beer). Thank you!

**PayPal**

* **[Donate $5]**: Thank's for creating this project, here's a coffee (or some beer) for you!

* **[Donate $10]**: Wow, I am stunned. Let me take you to the movies!ù

* **[Donate $15]**: I really appreciate your work, let's grab some lunch!

* **[Donate $25]**: That's some awesome stuff you did right there, dinner is on me!

* **[Donate $50]**: I really really want to support this project, great job!

* **[Donate $100]**: You are the man! This project saved me hours (if not days) of struggle and hard work, simply awesome!

* **[Donate $2799]**: Go buddy, buy Macbook Pro for yourself!

Of course, you can also choose what you want to donate, all donations are awesome!!


#Start from

minSdkVersion 14

#LICENSE

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

#Authors

[Saveen Dhiman] original Author


[Donate $5]: 		https://www.paypal.me/saveendhiman/5
[Donate $10]:  		https://www.paypal.me/saveendhiman/10
[Donate $15]:  		https://www.paypal.me/saveendhiman/15
[Donate $25]:  		https://www.paypal.me/saveendhiman/25
[Donate $50]: 		https://www.paypal.me/saveendhiman/50
[Donate $100]: 		https://www.paypal.me/saveendhiman/100
[Donate $2799]: 	https://www.paypal.me/saveendhiman/2799

[Saveen Dhiman]:        https://github.com/saveendhiman

[Retrofit2]: 		https://square.github.io/retrofit
[RX java]:		https://github.com/ReactiveX/RxJava
[Dagger2]: 		https://google.github.io/dagger
[Firebase]:             https://firebase.google.com
[Calligraphy]:          https://github.com/chrisjenx/Calligraphy
[Picasso]:              http://square.github.io/picasso
[Komensky]:             https://github.com/inmite/android-validation-komensky
[Fabric]:               https://get.fabric.io/#
[Butterknife]:          http://jakewharton.github.io/butterknife
[Timber]:               https://github.com/JakeWharton/timber


