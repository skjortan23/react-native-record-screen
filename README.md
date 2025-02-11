[![Stand With Ukraine](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://stand-with-ukraine.pp.ua)

# react-native-record-screen

A screen record module for React Native.

- Support iOS >= 11.0 (Simulator is not work)

- Support Android
  - minSdkVersion = 21
  - compileSdkVersion = 29
  - targetSdkVersion = 29
  - use [HBRecorder](https://github.com/HBiSoft/HBRecorder)

## Installation

### iOS

```sh
npm install react-native-record-screen
```

Add the permission strings to your Info.plist

```xml
<key>NSCameraUsageDescription</key>
<string>Please allow use of camera</string>
<!-- If you intend to use the microphone -->
<key>NSMicrophoneUsageDescription</key>
<string>Please allow use of microphone</string>
```

pod install

```sh
npx pod-install
```

### Android

Add the permissions to your AndroidManifest.xml

```xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_INTERNAL_STORAGE" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<!-- If you intend to use the microphone -->
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

## Usage

### Recording full screen

```js
import RecordScreen, { RecordingStartResponse } from 'react-native-record-screen';

// recording start
const res = RecordScreen.startRecording().catch((error) => console.error(error));
if (res === RecordingStartResponse.PermissionError) {
  // user denies access
}

// recording stop
const res = await RecordScreen.stopRecording().catch((error) =>
  console.warn(error)
);
if (res) {
  const url = res.result.outputURL;
}
```

### Setting microphone

default true.

```js
// mic off
RecordScreen.startRecording({ mic: false }).catch((error) =>
  console.error(error)
);

// recording stop
const res = await RecordScreen.stopRecording().catch((error) =>
  console.warn(error)
);
if (res) {
  const url = res.result.outputURL;
}
```

### Adjusting bitrate / frame rate

```js
RecordScreen.startRecording({
  bitrate: 1024000, // default 236390400
  fps: 24, // default 60
})
```

### Clean Sandbox

```js
RecordScreen.clean();
```

## License

MIT
