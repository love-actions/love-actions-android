# love-actions-android

## About

Github Action for building & deploying Android `.apk` and `.abb` packages of a [LÖVE](https://love2d.org/) framework based game.

### Related actions

See related actions below:

[Love actions bare package](https://github.com/marketplace/actions/love-actions-bare-package)

[Love actions for testing](https://github.com/marketplace/actions/love-actions-for-testing)

[Love actions for iOS](https://github.com/marketplace/actions/love-actions-for-ios)

[Love actions for Linux](https://github.com/marketplace/actions/love-actions-for-linux)

[Love actions for macOS](https://github.com/marketplace/actions/love-actions-for-macos)

[Love actions for Windows](https://github.com/marketplace/actions/love-actions-for-windows)

## Quick example

```yaml
- name: Build love android
  id: build-love
  uses: 26F-Studio/love-actions-android@main
  with:
    app-name: "My Love Game"
    bundle-id: "org.love2d.my_game"
    keystore-alias: ${{ secrets.ANDROID_KEYSTORE_ALIAS }}
    keystore-base64: ${{ secrets.ANDROID_KEYSTORE_BASE64 }}
    keystore-key-password: ${{ secrets.ANDROID_KEYSTORE_KEYPASSWORD }}
    keystore-store-password: ${{ secrets.ANDROID_KEYSTORE_STOREPASSWORD }}
    love-package: "./game.love"
    product-name: "my-game"
    resource-path: "./assets/android/res"
    version-string: "2.3.4"
    version-code: 234
    output-folder: "./dist"
```

## All inputs

| Name                      | Required | Default                | Description                                                  |
| :------------------------ | -------- | ---------------------- | ------------------------------------------------------------ |
| `app-name`                | `false`  | `"LÖVE for Android"`   | App display name, used in `app/src/main/AndroidManifest.xml` |
| `bundle-id`               | `false`  | `"org.love2d.android"` | App bundle id, used in `app/build.gradle`                    |
| `icon-specifier`          | `false`  | `"@drawable/love"`     | App icon specifier used in `app/src/main/AndroidManifest.xml` |
| `keystore-alias`          | `false`  | `""`                   | Signing keystore's alias, won't build release packages if not specified |
| `keystore-base64`         | `false`  | `""`                   | Signing keystore's content in `base64` string, won't build release packages if not specified |
| `keystore-key-password`   | `false`  | `""`                   | Signing keystore's key password, won't build release packages if not specified |
| `keystore-store-password` | `false`  | `""`                   | Signing keystore's store password, won't build release packages if not specified |
| `love-package`            | `false`  | `"./game.love"`        | `.love` game package file path                               |
| `product-name`            | `false`  | `"love-app"`           | Base name of the package. Used to rename products            |
| `resource-path`           | `true`   | `""`                   | Path to the android resources folder, would copy all contents to `app/src/main/res` exclude top folder |
| `version-string`          | `false`  | `"11.4"`               | App version string no more than 3 numbers, used in `app/build.gradle` |
| `version-code`            | `false`  | `"30"`                 | Numeric app version code , used in `app/build.gradle`        |
| `output-folder`           | `false`  | `"./build"`            | Built packages output folder                                 |

## All outputs

| Name            | Example                                                      | Description                                                  |
| :-------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `package-paths` | `./build/app-embed-record-debug.apk ./build/app-embed-record-release.apk` | built packages' paths in a bash-style list relative to the repository root, separated by spaces |
