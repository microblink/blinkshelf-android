# Custom UX 

Customization can be achieved by passing the `Theme` object to the `CameraSettings` which is used when instantiating fragments as described on the Getting Started [page](getting_started.md#usage).

An example of customization is shown in the code sample below.


```kotlin
val options = CameraSettings {
    theme(
        Theme(
            ThemeColors {
                primaryColor(0xFF_682_28B)      // purple  
                secondaryColor(0xFF_7FF_F00)    // green
                textColor(0xFF_FF5_733)         // orange
            }
        )
    )
}
```

The following sections contain screenshots of how customization from above affects different parts of the UI. 


## Scanning image banner
| Default     | Custom |
| ----------- | ----------- |
| ![scanning_image_banner_default](images/customization/default/scanning_image_banner_default.png)  | ![scanning_image_banner_custom](images/customization/custom/scanning_image_banner_custom.png) |

## Results screen
| Default     | Custom |
| ----------- | ----------- |
| ![results_screen_default](images/customization/default/results_screen_default.png)  | ![results_screen_custom](images/customization/custom/results_screen_custom.png) |

## Bottom sheet with a list of the promotion results
| Default     | Custom |
| ----------- | ----------- |
| ![bottom_sheet_results_list_default](images/customization/default/bottom_sheet_results_list_default.png)  | ![bottom_sheet_results_list_custom](images/customization/custom/bottom_sheet_results_list_custom.png) |

## Bottom sheet with promotion's details
| Default     | Custom |
| ----------- | ----------- |
| ![bottom_sheet_promo_details_default](images/customization/default/bottom_sheet_promo_details_default.png)  | ![bottom_sheet_promo_details_custom](images/customization/custom/bottom_sheet_promo_details_custom.png) |

## No promotions banner
| Default     | Custom |
| ----------- | ----------- |
| ![no_promo_banner_default](images/customization/default/no_promo_banner_default.png)  | ![no_promo_banner_custom](images/customization/custom/no_promo_banner_custom.png) |

## Permission screen
| Default     | Custom |
| ----------- | ----------- |
| ![permission_screen_default](images/customization/default/permission_screen_default.png)  | ![permission_screen_custom](images/customization/custom/permission_screen_custom.png) |

  