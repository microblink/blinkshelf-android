# Getting Started

## Project Integration and Initialization
To add SDK to your Android project, please follow the instructions below.

In your `build.gradle`, add Microblink maven repository to repositories list

```groovy
repositories {
    maven { url 'https://maven.microblink.com' }
}
```

Add dependencies

```groovy
dependencies {
    def sdk_version = "1.0.0"
    implementation("com.microblink.recognition:blinkshelf-core:$sdk_version") 
    implementation("com.microblink.recognition:blinkshelf-camera:$sdk_version") 
    implementation("com.microblink.recognition:blinkshelf-camera-ui:$sdk_version") 
    
    // optional, required when using store detection feature
    implementation("com.google.android.gms:play-services-location:21.0.1")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-play-services:1.7.3")
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

More info about defining [`RecognitionSettings`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-recognition-settings/index.html) can be found [here](sdk_options.md#recognition-settings).


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


