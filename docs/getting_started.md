# Getting Started


## AAR
Android Archive (AAR) containing everything needed to use the BlinkShelf library can be retrieved from [here](https://github.com/microblink/blinkshelf-android){target=_blank}.


## Project Integration and Initialization
To add SDK to your Android project, please add the following to your dependency section in your app `build.gradle`.
```groovy
dependencies {
    implementation("androidx.core:core-ktx:1.9.0")
    implementation("androidx.appcompat:appcompat:1.5.1")
    implementation("androidx.datastore:datastore-preferences:1.0.0")

    implementation("com.google.android.material:material:1.7.0")

    implementation("io.ktor:ktor-client-okhttp:2.1.3")
    implementation("io.ktor:ktor-client-android:2.1.3")
    implementation("io.ktor:ktor-serialization-kotlinx-json:2.1.3")
    implementation("io.ktor:ktor-client-logging:2.1.3")
    implementation("io.ktor:ktor-client-content-negotiation:2.1.3")
    implementation("io.ktor:ktor-client-auth:2.1.3")

    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.4")

    implementation("com.squareup.okio:okio:3.2.0")
    implementation("com.squareup.logcat:logcat:0.1")

    implementation(platform("androidx.compose:compose-bom:2022.11.00"))
    implementation("androidx.compose.ui:ui")
    implementation("androidx.compose.ui:ui-tooling")
    implementation("androidx.compose.foundation:foundation")
    implementation("androidx.compose.material:material")
    implementation("androidx.compose.material:material-icons-core")
    implementation("androidx.compose.material:material-icons-extended")
    implementation("androidx.activity:activity-compose:1.6.1")
    implementation("androidx.constraintlayout:constraintlayout-compose:1.0.1")
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.5.1")

    implementation("androidx.camera:camera-core:1.2.0-rc01")
    implementation("androidx.camera:camera-camera2:1.2.0-rc01")
    implementation("androidx.fragment:fragment-ktx:1.5.4")
    implementation("androidx.camera:camera-lifecycle:1.2.0-rc01")
    implementation("androidx.camera:camera-video:1.2.0-rc01")
    implementation("androidx.camera:camera-view:1.2.0-rc01")
    implementation("androidx.camera:camera-extensions:1.2.0-rc01")

    implementation("com.google.accompanist:accompanist-pager:0.27.0")
    implementation("com.google.accompanist:accompanist-pager-indicators:0.27.0")
    implementation("com.google.accompanist:accompanist-permissions:0.27.0")

    implementation("io.coil-kt:coil:2.2.2")
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
The easiest way to get started is to use the internal `CameraFragment`.
```xml
<androidx.fragment.app.FragmentContainerView
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/fragmentContainerView"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

```kotlin
val options = CameraSettings {
    // define customizable settings if needed 
}

supportFragmentManager
    .beginTransaction()
    .add(
        R.id.fragmentContainerView,
        CameraFragment.newInstance(options),
        null
    )
    .commit()
```

More info about defining Camera Settings can be found [here](fundamentals.md#scanning-options).


### Handling results
`CameraFragment` uses [Fragment Result API](https://developer.android.com/guide/fragments/communicate#fragment-result){target=_blank} to send results back to the calling Activity. To get results, the client must set `FragmentResultListener` as shown in the code below:
```kotlin
supportFragmentManager
    .setFragmentResultListener(CameraFragment.REQUEST_KEY, this) { _, bundle ->
        val result = CameraBundle.unwrap(bundle)
        // do something with results
    }
```
Results are wrapped in the bundle and can easily be unwrapped using the built-in helper method `CameraBundle.unwrap()`.


