# XCCOV Parser

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

## TODO:
- [ ] Fancier output
- [ ] Integration in Danger