# App Bundle Overview

## Usual Apk Contents
    AndroidManifest.xml
    classes
    resources.asrc
    res/
    assets/
    lib/
    META-INF/
    ...

## Bundle Contents
    base/
        dex/
        lib/            - abi related
        resources.pb    - strings etc.
        res/            - density related
        assets/
        root/
        META-INF/
        native.pb
        assets.pb
        manifest/
        ...
    BUNDLE-METADATA/
    BundleConfig.pb
    META-INF/

## All Apks Generated From Bundle
    splits/         - fragments of apk divided according to bundle{} in app/build.gradle
        master      - master apk contents that does not depend on splits
        density     - screen size disparitions
        language
        abi
        dynamicFeatures
    toc.pb          - all variants and app descriptions

## Universel(Single) Apks Contents
    universal.apk
    toc.pb

## bundletool(Generate Apk from bundle)
    Tool to generate apk content from bundle, useful options are shown below:

    --bundle=path (required)
    --output=path (required)
    --mode=universal (optional)
    --device-spec=spec_json (optional)
    --connected-device (optional)

    Usage

        Build Apks:
            bundletool build-apks --connected-device
            bundletool build-apks --device-spec=/MyApp/pixel2.json

        Device Spec:
            bundletool get-device-spec --output=/tmp/device-spec.json

        Extract(NOT TESTED)
            bundletool extract-apks
            --apks=/MyApp/my_existing_APK_set.apks
            --output-dir=/MyApp/my_pixel2_APK_set.apks
            --device-spec=/MyApp/bundletool/pixel2.json

## How to Read .pb Files(change inputs accordingly)
    protoc --experimental_allow_proto3_optional \
       --proto_path=proto \
       --decode=android.bundle.BuildApksResult \
       commands.proto \
        < /home/koray/AndroidStudioProjects/MyApplication/toc.pb > toc.raw

## Resources from Apk(for comparison)
    aapt2 dump resources example.apk > example.apk.rscdump

