# Getting Started


## AAR
Android Archive (AAR) containing everything needed to use the BlinkShelf library can be retrieved from [here](https://github.com/microblink/blinkshelf-android){target=_blank}.


## Project Integration and Initialization
To add SDK to your Android project, please add the following to your dependency section in your app `build.gradle`.
```groovy
dependencies {
    implementation("androidx.core:core-ktx:1.9.0")
    implementation("androidx.appcompat:appcompat:1.6.0")
    implementation("androidx.datastore:datastore-preferences:1.0.0")
    implementation("androidx.fragment:fragment-ktx:1.5.5")

    implementation("com.google.android.material:material:1.8.0")

    implementation("io.ktor:ktor-client-okhttp:2.2.3")
    implementation("io.ktor:ktor-client-android:2.2.3")
    implementation("io.ktor:ktor-serialization-kotlinx-json:2.2.3")
    implementation("io.ktor:ktor-client-logging:2.2.3")
    implementation("io.ktor:ktor-client-content-negotiation:2.2.3")
    implementation("io.ktor:ktor-client-auth:2.2.3")

    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.4")

    implementation("com.squareup.okio:okio:3.3.0")
    implementation("com.squareup.logcat:logcat:0.1")

    implementation(platform("androidx.compose:compose-bom:2023.01.00"))
    implementation("androidx.compose.ui:ui")
    implementation("androidx.compose.ui:ui-tooling")
    implementation("androidx.compose.foundation:foundation")
    implementation("androidx.compose.material:material")
    
    implementation("androidx.camera:camera-core:1.2.1")
    implementation("androidx.camera:camera-camera2:1.2.1")
    implementation("androidx.camera:camera-lifecycle:1.2.1")
    implementation("androidx.camera:camera-view:1.2.1")

    implementation("com.google.accompanist:accompanist-pager:0.28.0")
    implementation("com.google.accompanist:accompanist-pager-indicators:0.28.0")
    implementation("com.google.accompanist:accompanist-permissions:0.28.0")

    implementation("io.coil-kt:coil-compose:2.2.2")

    implementation("com.airbnb.android:lottie:5.2.0")
    implementation("com.airbnb.android:lottie-compose:5.2.0")


    implementation(project(":recognition-core"))
    implementation(project(":recognition-camera"))
    implementation(project(":recognition-camera-ui"))
}
```


## Set up License Key 
The recommended way to initialize the SDK would be through the `AndroidManifest.xml` file. Within this file, add the following configuration.

```xml
 <meta-data
    android:name="com.microblink.recognition.License"
    android:value="LICENSE KEY" />
```

## Usage
The easiest way to get started is to use the internal [`RecognitionFragment`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-recognition-fragment/index.html).
```xml
<androidx.fragment.app.FragmentContainerView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/fragmentContainerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

```kotlin
val settings = RecognitionSettings {
    // define customizable settings if needed 
}

supportFragmentManager
    .beginTransaction()
    .add(
        R.id.fragmentContainerView,
        RecognitionFragment.newInstance(settings),
        null
    )
    .commit()
```

More info about defining [`RecognitionSettings`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-recognition-settings/index.html) can be found [here](fundamentals.md#recognition-settings).


### Handling results
[`RecognitionFragment`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-recognition-fragment/index.html) uses [Fragment Result API](https://developer.android.com/guide/fragments/communicate#fragment-result){target=_blank} to send results back to the calling Activity. To get results, the client must set `FragmentResultListener` as shown in the code below. It is possible to listen to results returned from the Product Recognition API and/or camera frames provided by the camera.

```kotlin
supportFragmentManager
    .setFragmentResultListener(
        RecognitionFragment.PRODUCTS_REQUEST_KEY,
        this
    ) { _, bundle ->
        val result: Products = ProductsBundle.unwrap(bundle)
        // do something with Products results
    }

supportFragmentManager
    .setFragmentResultListener(
        RecognitionFragment.MEDIA_REQUEST_KEY,
        this
    ) { _, bundle ->
        val result: Media = MediaBundle.unwrap(bundle)
        // do something with Media results
    }
```

Results are wrapped in the bundle and can easily be unwrapped using the built-in helper method.


