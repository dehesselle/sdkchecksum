# macOS SDK checksums

Apple does not provide public downloads of macOS SDKs. That is a problem if you need a specific SDK for your public builds. You can either use existing unofficial sources or provide one yourself. Despite potential legal issues, how to make this trustworthy in the eyes of others?

This repository provides instructions on how to checksum and verify SDKs.

A full list of Xcode and SDK versions can be found on [Wikipedia](https://en.wikipedia.org/wiki/Xcode).

## MacOSX10.11.4.sdk (15E60)

1. Download `Xcode_7.3.1.dmg` and verify checksum.

   ```bash
   # expected checksum: bb0dedf613e86ecb46ced945913fa5069ab716a0ade1035e239d70dee0b2de1b
   shasum -a 256 Xcode_7.3.1.dmg
   ```

1. Mount with `open Xcode_7.3.1.dmg` and verify the version numbers.

   ```bash
   # expected output: 7.3.1
   /usr/libexec/PlistBuddy -c "Print :CFBundleShortVersionString" /Volumes/Xcode/Xcode.app/Contents/Info.plist
   # expected output: 7D1012
   /usr/libexec/PlistBuddy -c "Print :DTXcodeBuild" /Volumes/Xcode/Xcode.app/Contents/Info.plist
   # expected output: 10.11.4
   /usr/libexec/PlistBuddy -c "Print :ProductVersion" /Volumes/Xcode/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/CoreServices/SystemVersion.plist
   # expected output: 15E60
   /usr/libexec/PlistBuddy -c "Print :ProductBuildVersion" /Volumes/Xcode/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/CoreServices/SystemVersion.plist
   ```

1. Create checksums of all files inside the SDK.

   ```bash
   cd /Volumes/Xcode/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs
   find MacOSX10.11.sdk -type f -exec shasum -a 256 {} + | LC_ALL=C sort > $HOME/MacOSX10.11.4.sdk.sha256
   # expected checksum: 52e2abff5e6411f684e3ecc266b20f10867df7e51d14247e473799efe6b6fcc2
   shasum -a 256 $HOME/MacOSX10.11.4.sdk.sha256
   ```

1. Wherever you need to verify the SDK, copy `MacOSX10.11.4.sdk.sha256` to the SDK's parent folder, `cd` to the parent folder and run the following command.

   ```bash
   # expected output: rc=0
   shasum -s -c MacOSX10.11.4.sdk.sha256; echo rc=$?
   ```

## MacOSX10.13.4.sdk (17E189)

1. Download `Xcode_9.4.1.xip` and verify checksum.

   ```bash
   # expected checksum: 7a338620ed3d225f675a74eb41925937fb90478b510b65b2b32e89c26be23124
   shasum -a 256 Xcode_9.4.1.xip
   ```

1. Extract to a location of your choice with `xip -x Xcode_9.4.1.xip` and verify the version numbers.

   ```bash
   # expected output: 9.4.1
   /usr/libexec/PlistBuddy -c "Print :CFBundleShortVersionString" Xcode.app/Contents/Info.plist
   # expected output: 9F1027a
   /usr/libexec/PlistBuddy -c "Print :DTXcodeBuild" Xcode.app/Contents/Info.plist
   # expected output: 10.13.4
   /usr/libexec/PlistBuddy -c "Print :ProductVersion" Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/CoreServices/SystemVersion.plist
   # expected output: 17E189
   /usr/libexec/PlistBuddy -c "Print :ProductBuildVersion" Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/CoreServices/SystemVersion.plist
   ```

1. Create checksums of all files inside the SDK.

   ```bash
   cd Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs
   find MacOSX10.13.sdk/ -type f -exec shasum -a 256 {} + | LC_ALL=C sort > $HOME/MacOSX10.13.4.sdk.sha256
   # expected checksum: eb09dd197b055e6d58061499bf54d9bebc8f572ab24e2e42424fa24991f050a2
   shasum -a 256 $HOME/MacOSX10.13.4.sdk.sha256
   ```

1. Wherever you need to verify the SDK, copy `MacOSX10.13.4.sdk.sha256` to the SDK's parent folder, `cd` to the parent folder and run the following command.

   ```bash
   # expected output: rc=0
   shasum -s -c MacOSX10.13.4.sdk.sha256; echo rc=$?
   ```

## MacOSX10.15.6.sdk (19G68)

1. Download `Xcode_12.1.xip` and verify checksum.

   ```bash
   # expected checksum: 612443b1894b39368a596ea1607f30cbb0481ad44d5e29c75edb71a6d2cf050f
   shasum -a 256 Xcode_12.1.xip
   ```

1. Extract to a location of your choice with `xip -x Xcode_12.1.xip` and verify the version numbers.

   ```bash
   # expected output: 12.1
   /usr/libexec/PlistBuddy -c "Print :CFBundleShortVersionString" Xcode.app/Contents/Info.plist
   # expected output: 12A7402d
   /usr/libexec/PlistBuddy -c "Print :DTXcodeBuild" Xcode.app/Contents/Info.plist
   # expected output: 10.15.6
   /usr/libexec/PlistBuddy -c "Print :ProductVersion" Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.15.sdk/System/Library/CoreServices/SystemVersion.plist
   # expected output: 19G68
   /usr/libexec/PlistBuddy -c "Print :ProductBuildVersion" Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.15.sdk/System/Library/CoreServices/SystemVersion.plist
   ```

1. Create checksums of all files inside the SDK.

   ```bash
   cd Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs
   find MacOSX10.15.sdk/ -type f -exec shasum -a 256 {} + | LC_ALL=C sort > $HOME/MacOSX10.15.6.sdk.sha256
   # expected checksum: 7733a568a494adeb2ac644017ab5a10818251e4c3e22c64c9bdb98dfa701a03a
   shasum -a 256 $HOME/MacOSX10.15.6.sdk.sha256
   ```

1. Wherever you need to verify the SDK, copy `MacOSX10.15.6.sdk.sha256` to the SDK's parent folder, `cd` to the parent folder and run the following command.

   ```bash
   # expected output: rc=0
   shasum -s -c MacOSX10.15.6.sdk.sha256; echo rc=$?
   ```

## License

[MIT](LICENSE)
