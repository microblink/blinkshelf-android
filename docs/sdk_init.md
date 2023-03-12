# SDK Initialization
The recommended way to initialize the SDK is by adding a License key in the `AndroidManifest.xml` file.
```xml
 <meta-data
    android:name="com.microblink.recognition.License"
    android:value="LICENSE KEY" />
```

By doing so, our content provider will be used, and it will automatically initialize all that is necessary for the SDK to work.

## Manual initialization
If you want to manually initialize the SDK, first, you should remove our content provider from the `AndroidManifest.xml` file, as shown in the snippet below.

```xml
<provider
    android:name="com.microblink.recognition.core.RecognitionProvider"
    android:authorities="${applicationId}.RecognitionProvider"
    tools:node="remove" />
```

After that, you should call `BlinkRecognitionSdk.initialize()` to initialize the SDK. There are a couple of ways how this can be achieved, we recommend using [App Startup](https://developer.android.com/topic/libraries/app-startup). Another way is to add the initialization code in the `Application` class in the `onCreate` method. 

The license key should be set in `AndroidManifest.xml` as mentioned in the section [above](#sdk-initialization).
