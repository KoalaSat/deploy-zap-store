# deploy-zap-store

This action sets up and deploys you APK to the [Zap.Store](https://github.com/zapstore/zapstore):
 - Downloading the SDK commandline tools, if the current version (11.0) is not found in either `$ANDROID_SDK_ROOT` or `$HOME/.android/sdk`.
 - Accepting the SDK licenses.
 - Installing `tools` and `platform-tools`.
 - Downloadin and Installing Dart SDK
 - Downloadin and Installing Apktool
 - Downloadin and Installing zapstore-cli
 - Setting up a new release and publishing it to nostr

# Pre-requisites

This action will deploy the latest release on your github repository. If you want to integrate it on your release workwlof make sure you run it after the release is created on GitHub.

# Usage

See [action.yml](action.yml)

## Basic
```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v4
        
  - name: Setup JDK 17
    uses: actions/setup-java@v4
    .....

  - name: Build APK
    run: ./gradlew assembleRelease --stacktrace

  - name: Sign APK
    uses: r0adkll/sign-android-release@v1
    .....

  - name: Create Release
    uses: actions/create-release@v1
    .....

  - name: Upload APK Universal Asset
    uses: actions/upload-release-asset@v1
    ....

  - name: Upload to zap.Store
    uses: KoalaSat/deploy-zap-store@v1
    with:
      app_name: Facy App
      nsec: ${{ secrets.NSEC }}
      api_version: 34
      build_tools_version: 34.0.0
```
