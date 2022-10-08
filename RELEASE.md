# Release

This file will indicate the process related to release

>> Note that the publishing is done in here through cocoapods, if you want alternative solutions
> please open an issue for it in this repository stating your preferred service


# Steps

Please follow these Steps in order to release:

**1**. Archive

You can either:

  **A**.  Directly through xcode gui:

        **I**. Toggle to device (Make you're not selecting a simulator)

        **II**. Then select product -> archive

  **B**.  Or in order to get an XCframework:

        Just run the below from terminal in the directory of the SDK

```

# iOS devices
xcodebuild archive \
-scheme MobAdSDK \
-archivePath "archives/MobAdSDK.xcarchive" \
-destination "generic/platform=iOS" \
-sdk iphoneos \
SKIP_INSTALL=NO \
BUILD_LIBRARY_FOR_DISTRIBUTION=YES

# iOS simulators
xcodebuild archive \
-scheme MobAdSDK \
-archivePath "archives/MobAdSDK-simulator.xcarchive" \
-destination "generic/platform=iOS Simulator" \
-sdk iphonesimulator \
SKIP_INSTALL=NO \
BUILD_LIBRARY_FOR_DISTRIBUTION=YES

xcodebuild -create-xcframework \
-framework "archives/MobAdSDK.xcarchive/Products/Library/Frameworks/MobAdSDK.framework" \
-framework "archives/MobAdSDK-simulator.xcarchive/Products/Library/Frameworks/MobAdSDK.framework" \
-output "MobAdSDK.xcframework"

```


**2**. Move generated .framework or .xcframework file to a new folder named: "FrameworkName"-"FrameworkVersion" example: NewFramework-1.1.0

**3**. Zip the new folder while preserving the format

**4**. Now cocoapods comes into place

   **A**. Check if pod is validated

```

   pod spec lint
   
```

   **B**. Push pod

```

   pod trunk push "FrameworkName".podspec

```


# References:

**1**. https://notificare.com/blog/2021/04/23/Publishing-XCFrameworks-via-CocoaPods/

**2**. https://notificare.com/blog/2020/12/11/Publishing-Binaries-with-SPM/

**3**. https://medium.com/@mkeremkeskin/distributing-closed-source-frameworks-with-cocoapods-and-carthage-44fd141cfd78