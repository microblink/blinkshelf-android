# Fundamentals


## SDK Initialization
The recommended way to initialize the SDK is by adding a License key in the `AndroidManifest.xml` file.
```xml
 <meta-data
   android:name="com.microblink.recognition.License"
   android:value="LICENSE KEY" />
```

By doing so, our content provider will be used, and it will automatically initialize all that is necessary for the SDK to work.

### Manual initialization
If you want to manually initialize the SDK, first, you should remove our content provider from the `AndroidManifest.xml` file, as shown in the snippet below.

```xml
<provider
   android:name="com.microblink.recognition.core.RecognitionProvider"
   android:authorities="${applicationId}.RecognitionProvider"
   tools:node="remove" />
```

After that, you should call `RecognitionSdk.initialize()` to initialize the SDK. There are a couple of ways how this can be achieved, we recommend using [App Startup](https://developer.android.com/topic/libraries/app-startup). Another way is to add the initialization code in the `Application` class in the `onCreate` method. 

The license key should be set in `AndroidManifest.xml` as mentioned in the section [above](#sdk-initialization).


## Scanning options
The SDK's Camera Fragment allows customizing built-in experience via `CameraSettings`. Values that can be customized are:

- camera resolution
- region of interest
- theme
- media options.

### Capture Resolution
Camera resolution can be set to any of the predefined resolutions defined in [`CameraResolution`](). If not set, it will default to 1080p.

### Region Of Interest
Defines the region in which we want to scan the frame. The properties of the `RectF` are defined as a percentage of the screen. If not set, the whole image will be used.

### Theme
Custom Theme can be set. This allows clients to define their brand's colors which will then be applied to the built-in scanning experience. If not set, the default theme and colors will be used. More info about customization can be found in [Custom UX](custom_ux.md).

### Media Options
By defining `MediaOptions`, it is possible to specify directory where captured images should be saved. `MediaOptions` contains a `File` object that should point to the desired folder. Note that provided folder should be part of app-specific files. If this option is not set, captured images will be saved in the default folder defined by the SDK.

Through `MediaOptions` it is also possible to set the desired format of the captured image, the currently supported value is JPEG.
