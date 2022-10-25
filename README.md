# love-actions-android

## About

Github Action for building & deploying Android `.apk` and `.abb` packages of a [LÖVE](https://love2d.org/) framework based game.

### Related actions

See related actions below:

[Love actions bare package](https://github.com/marketplace/actions/love-actions-bare-package)

[Love actions for testing](https://github.com/marketplace/actions/love-actions-for-testing)

[Love actions for iOS](https://github.com/marketplace/actions/love-actions-for-ios)

[Love actions for Linux](https://github.com/marketplace/actions/love-actions-for-linux)

[Love actions for macOS portable](https://github.com/marketplace/actions/love-actions-for-macos-portable)

[Love actions for macOS App Store](https://github.com/marketplace/actions/love-actions-for-macos-app-store)

[Love actions for Windows](https://github.com/marketplace/actions/love-actions-for-windows)

## Quick example

```yaml
- name: Build love android
  id: build-love
  uses: love-actions/love-actions-android@v1
  with:
    app-name: "My Love Game"
    bundle-id: "org.love2d.my_game"
    resource-path: "./assets/android/res"
    icon-specifier: "@mipmap/app"
    love-ref: "11.4"
    love-patch: "./love.patch"
    love-package: "./game.love"
    libs-path: "./assets/android/libs"
    extra-assets: ./README.md ./license.txt
    product-name: "my-game"
    version-string: "2.3.4"
    version-code: 234
    output-folder: "./dist"
    keystore-alias: ${{ secrets.ANDROID_KEYSTORE_ALIAS }}
    keystore-base64: ${{ secrets.ANDROID_KEYSTORE_BASE64 }}
    keystore-key-password: ${{ secrets.ANDROID_KEYSTORE_KEYPASSWORD }}
    keystore-store-password: ${{ secrets.ANDROID_KEYSTORE_STOREPASSWORD }}
```

## All inputs

| Name                        | Required  | Default                  | Description                                                                                                                                                |
| :-------------------------- | --------- | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `app-name`                | `false` | `"LÖVE for Android"`  | App display name. Used in `app/src/main/AndroidManifest.xml`                                                                                             |
| `bundle-id`               | `false` | `"org.love2d.android"` | App bundle id. Used in `app/build.gradle`                                                                                                                |
| `resource-path`           | `true`  | `""`                   | Path to the android resources folder. Would copy all contents to `app/src/main/res` excluding top folder                                                 |
| `icon-specifier`          | `false` | `"@drawable/love"`     | App icon specifier. Used in `app/src/main/AndroidManifest.xml`                                                                                           |
| `love-ref`                | `false` | `"11.4"`               | `love-android` git ref. Could be commit hash, tags or branch name                                                                                        |
| `love-patch`              | `false` | `""`                   | Git patch file path for the `love-android` repo. The patch must start from `love-ref`. You can use `git diff -p <tag1> <tag2>` to get the patch file |
| `love-package`            | `false` | `"./game.love"`        | `.love` game package file path                                                                                                                           |
| `libs-path`               | `false` | `""`                   | Path to the JNI libraries folder. Would copy all contents to `app/libs` excluding top folder                                                             |
| `extra-assets`            | `false` | `""`                   | List of folder & file paths to be added to `app/src/embed/assets/`. Separated by spaces                                                                  |
| `product-name`            | `false` | `"love-app"`           | Base name of the package. Used to rename products                                                                                                          |
| `version-string`          | `false` | `"11.4"`               | App version string no more than 3 numbers. Used in `app/build.gradle`                                                                                    |
| `version-code`            | `false` | `"30"`                 | Numeric app version code . Used in `app/build.gradle`                                                                                                    |
| `output-folder`           | `false` | `"./build"`            | Built packages output folder                                                                                                                               |
| `keystore-alias`          | `false` | `""`                   | Signing keystore's alias. Won't build release packages if not specified                                                                                    |
| `keystore-base64`         | `false` | `""`                   | Signing keystore's content in `base64` string. Won't build release packages if not specified                                                             |
| `keystore-key-password`   | `false` | `""`                   | Signing keystore's key password. Won't build release packages if not specified                                                                             |
| `keystore-store-password` | `false` | `""`                   | Signing keystore's store password. Won't build release packages if not specified                                                                           |

## All outputs

| Name              | Example                                                   | Description                                                                                     |
| :---------------- | --------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `package-paths` | `./build/my-game-debug.apk ./build/my-game-release.apk` | Built packages' paths in a bash-style list relative to the repository root, separated by spaces |
