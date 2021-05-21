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

## License

[MIT](LICENSE)
