# Segment-Apptimize

[![CI Status](http://img.shields.io/travis/segment-integrations/analytics-ios-integration-apptimize.svg?style=flat)](https://travis-ci.org/segment-integrations/analytics-ios-integration-apptimize)
[![Version](https://img.shields.io/cocoapods/v/Segment-Apptimize.svg?style=flat)](http://cocoapods.org/pods/Segment-Apptimize)
[![License](https://img.shields.io/cocoapods/l/Segment-Apptimize.svg?style=flat)](http://cocoapods.org/pods/Segment-Apptimize)

Apptimize integration for [analytics-ios](https://github.com/segmentio/analytics-ios).

## Installation

Analytics is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your `Podfile`:

```ruby
pod "Segment-Apptimize"
```

## Usage

After adding the dependency, you must register the integration with our SDK. To do this, import the Apptimize integration in your AppDelegate:


```
#import <Segment-Apptimize/SEGApptimizeIntegrationFactory.h>
```

And add the following lines:

```
NSString *const SEGMENT_WRITE_KEY = @" ... ";
SEGAnalyticsConfiguration *config = [SEGAnalyticsConfiguration configurationWithWriteKey:SEGMENT_WRITE_KEY];

[config use:[SEGApptimizeIntegrationFactory instance]];

[SEGAnalytics setupWithConfiguration:config];
```

If you encounter issues deploying to the AppStore, add the following script
to the end of your build phases:

```
echo "Checking for and embedding required swift librarires"

SCAN_PATHS=`find "${TARGET_BUILD_DIR}" -type d -name '*Apptimize*.framework' | sed -E 's|/[^/]+$||' | sed -E 's|^(.*)$|--scan-folder '\''\1'\'' |' | sort -u | tr '\n' ' '`

$TOOLCHAIN_DIR/usr/bin/swift-stdlib-tool \
   --copy --verbose --sign ${EXPANDED_CODE_SIGN_IDENTITY} \
   --scan-executable "${TARGET_BUILD_DIR}/${EXECUTABLE_PATH}" \
   $SCAN_PATHS \
   --platform ${PLATFORM_NAME} \
   --toolchain $TOOLCHAIN_DIR \
   --destination "${TARGET_BUILD_DIR}/${FRAMEWORKS_FOLDER_PATH}" \
   --resource-destination "${TARGET_BUILD_DIR}/${FULL_PRODUCT_NAME}" \
   --resource-library libswiftRemoteMirror.dylib
```

## License

```
WWWWWW||WWWWWW
 W W W||W W W
      ||
    ( OO )__________
     /  |           \
    /o o|    MIT     \
    \___/||_||__||_|| *
         || ||  || ||
        _||_|| _||_||
       (__|__|(__|__|

The MIT License (MIT)

Copyright (c) 2014 Segment, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
