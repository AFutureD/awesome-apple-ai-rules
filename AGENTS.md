---
description: Instructions For Agents, such as Cursor, Copilot, Codex.
---

# Basic Guide
- This is a iOS App project.
- The 'APP NAME', the xcworkspace 'TARGET', 'BUILD SCHEME' is called '[YOUR APP NAME]'
- This Project is using Cocopods as a dependency manager.

# Dev Environment Instructions
- Install 'swiftformat' as code formatter, link: https://github.com/nicklockwood/SwiftFormat
  - install command: `brew install swiftformat`
- Install mise decpendency if the exists
  - Test mise existence using command `command -v mise`
  - Install decpendency using command `mise install`
- Run `pod install` if 'Pods' not exists.

# Build Instructions
- run 'pod install' after each 'git pull' or 'git merge' command to resolve 'podfile.lock' issue
- Using the scheme 'FaceYoga' under the `@./[YOUR WORKSPACE].xcworkspace`
- Use the following command to build the target
  `xcodebuild -sdk iphoneos -workspace ./{{WORKSPACE NAME}}.xcworkspace -scheme {{BUILD SCHEME}} -destination 'generic/platform=iOS Simulator' -quiet -allowProvisioningUpdates -configuration Debug build`

# Launch App on Simulator Instructions
- Launch the Simulator App.
  - Command `open -g -a Simulator`
- Check if a device is 'Booted', and memorize the 'id'
  - Command `xcrun simctl list devices`
  - If multiple device found, choose the one with newest system version, 
    if the system version is the same choose a random one.
- Get app path and app product identifier
  - Get app path using comamnd: `xcodebuild -sdk iphoneos -workspace ./{{WORKSPACE NAME}}.xcworkspace -scheme {{BUILD SCHEME}} -destination 'generic/platform=iOS Simulator' -quiet -allowProvisioningUpdates -configuration Debug -showBuildSettings | grep 'CODESIGNING_FOLDER_PATH'`
  - Get app product identifier using comamnd: `xcodebuild -sdk iphoneos -workspace ./{{WORKSPACE NAME}}.xcworkspace -scheme {{BUILD SCHEME}} -destination 'generic/platform=iOS Simulator' -quiet -allowProvisioningUpdates -configuration Debug -showBuildSettings | grep 'PRODUCT_BUNDLE_IDENTIFIER'`
- Install app to the simualtor:
  - command: `xcrun simctl install {{Simulator ID}} '{{APP PATH}}'`
- Launch APP:
  - command: `xcrun simctl launch --console-pty --terminate-running-process {{Simulator ID}} {{APP PRODUCT IDENTIFIER}}`

# Build And Launch Exmaple
```sh
# Assume Develper enviroment are all set.

> xcodebuild -sdk iphoneos -workspace ./FaceYoga.xcworkspace -scheme FaceYoga -destination 'generic/platform=iOS Simulator' -quiet -allowProvisioningUpdates -configuration Debug Build

> open -g -a Simulator

> xcrun simctl list devices
== Devices ==
-- iOS 15.5 --
    iPhone 12 mini (390EF108-C375-468C-8D8D-45472C7A49D1) (Booted)
    iPhone 8 (CA534070-29CC-4736-89DC-8308D7E1A622) (Shutdown)
-- iOS 17.5 --
-- iOS 18.2 --
-- iOS 18.4 --
    iPhone 16 Pro (B2BEC6E0-838B-4A06-83B1-2970E7DAC8A7) (Shutdown)

> xcodebuild -sdk iphoneos -workspace ./FaceYoga.xcworkspace -scheme FaceYoga -destination 'generic/platform=iOS Simulator' -quiet -allowProvisioningUpdates -configuration Debug -showBuildSettings | grep 'CODESIGNING_FOLDER_PATH'
    CODESIGNING_FOLDER_PATH = /Users/huanan/Library/Developer/Xcode/DerivedData/FaceYoga-aqbixvrbpcnzamdamiamvzczcanc/Build/Products/Debug-iphonesimulator/FaceYoga.app

> xcodebuild -sdk iphoneos -workspace ./FaceYoga.xcworkspace -scheme FaceYoga -destination 'generic/platform=iOS Simulator' -quiet -allowProvisioningUpdates -configuration Debug -showBuildSettings | grep 'PRODUCT_BUNDLE_IDENTIFIER'
    PRODUCT_BUNDLE_IDENTIFIER = com.simplehealth.faceyoga

> xcrun simctl install 390EF108-C375-468C-8D8D-45472C7A49D1 /Users/huanan/Library/Developer/Xcode/DerivedData/FaceYoga-aqbixvrbpcnzamdamiamvzczcanc/Build/Products/Debug-iphonesimulator/FaceYoga.app

> xcrun simctl launch --console-pty --terminate-running-process 390EF108-C375-468C-8D8D-45472C7A49D1 com.simplehealth.faceyoga
```

