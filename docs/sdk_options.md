# Recognition settings
The SDK's Recognition Fragment allows customizing built-in experience via [`RecognitionSettings`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-recognition-settings/index.html). Values that can be customized are:

- camera resolution
- region of interest
- theme
- media options
- products options.

## Capture Resolution
Camera resolution can be set to any of the predefined resolutions defined in [`CameraResolution`](https://microblink.github.io/blinkshelf-android/javadocs/camera/recognition-camera/com.microblink.recognition.camera/-camera-resolution/index.html). If not set, it will default to 1080p.

## Region Of Interest
Defines the region in which we want to scan the frame. The properties of the `RectF` are defined as a percentage of the screen. If not set, the whole image will be used.

## Theme
Custom Theme can be set. This allows clients to define their brand's colors which will then be applied to the built-in scanning experience. If not set, the default theme and colors will be used. More info about customization can be found in [Theming](theming.md).

## Media Options
By defining [`MediaOptions`](https://microblink.github.io/blinkshelf-android/javadocs/camera/recognition-camera/com.microblink.recognition.camera/-media-options/index.html), it is possible to specify directory where captured images should be saved. `MediaOptions` contains a `File` object that should point to the desired folder. Note that provided folder should be part of app-specific files. If this option is not set, captured images will be saved in the default folder defined by the SDK.

Through `MediaOptions` it is also possible to set the desired format of the captured image, the currently supported value is JPEG.

## Products Options
SDK's results can be customized using [`ProductsOptions`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-products-options/index.html) class.

Field `country` sets which country should be used as product database source.
By default, United States is used, more info about other country options can be found [here](https://microblink.github.io/blinkshelf-android/javadocs/core/recognition-core/com.microblink.recognition.core/-country/index.html). 

By setting `shouldReturnPromotions` to `true`, clients can get both Promotions and Products in the result.
Otherwise, if `shouldReturnPromotions` flag is set to `false`, results will only include Promotions.
Note that the default SDK's UI will also be affected when using this flag.

[`StoreDetectionOptions`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-store-dection-options/index.html) class allows configuring store detection parameters.
Store detection is enabled by default, but it can be disabled by setting `enabled` to false. 
If enabled, it is possible to specify the radius within which store detection should be performed.
The default search radius is 1 mile. Both radius value and units can be configured.

[`FrameOptions`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-frame-options/index.html) allows setting frame compression 
parameters used for product recognition.
It is possible to set both compression quality and compression format. 
Compression quality must be larger than the specified [minimum compression quality value](https://microblink.github.io/blinkshelf-android/javadocs/core/recognition-core/com.microblink.recognition.core/-frame-quality/-m-i-n-_-q-u-a-l-i-t-y.html),
and less than 100. In case these conditions aren't met, SDK won't return results. 
Compression Format can be one of the values available in [`FrameFormat`](https://microblink.github.io/blinkshelf-android/javadocs/core/recognition-core/com.microblink.recognition.core/-frame-format/index.html).

## Ui Options
Out-of-the-box experience can be modified by settings [`UiOptions`](https://microblink.github.io/blinkshelf-android/javadocs/camera-ui/recognition-camera-ui/com.microblink.recognition.camera.ui/-ui-options/index.html).

`UiOptions` contain the flag `shouldShowSessionId` which allows the client to display the session ID on the UI. 
By default, the session ID won't be shown.