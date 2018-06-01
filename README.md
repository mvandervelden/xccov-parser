# XCCOV Parser

## Goal
The aim of this project is to have a light-weight code coverage parser that can run in CI and do a simple report to Github to track trends in code coverage on a PR basis. Now Xcode exposes it's own coverage reporting tooling `xccov` (starting with Xcode 9.3), this should not be hard to achieve. Using Danger, it should also be light-weight to report coverage back to Github while being agnostic of CI service being used.

The goal is not to have fancy trend analysis or full insight into coverage on line level, for the former, some service is required to store previous coverage on, for the latter it's easy enough to check Xcode for that.

## Usage
 ```sh
 #Compile your project with derived data going to `Build/`
 xcodebuild -workspace [YourWorkspace].xcworkspace -scheme [YourScheme] -derivedDataPath Build/ -destination 'platform=iOS Simulator,OS=11.4,name=iPhone 7' -enableCodeCoverage YES clean build test CODE_SIGN_IDENTITY="" CODE_SIGNING_REQUIRED=NO
#Generate coverage json
xcrun xccov view Build/Logs/Test/*.xccovreport --json > coverage.json
#Parse
swift Parser.swift coverage.json
 ```

## Output
```
Total coverage : 15.317%
 My.framework   : 70.508%
 Other.framework: 45.500%
 Third.framework: 43.277%
```

## Notes:
- It does not display Pods (except development Pods)
- It does not display test targets
- Inspired by: https://medium.com/xcblog/xccov-xcode-code-coverage-report-for-humans-466a4865aa18

## TODO:
- [ ] Fancier output
- [ ] Integration in Danger