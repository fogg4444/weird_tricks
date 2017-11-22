# React Native Development

---
### Fastlane gives error like: `Cannot proceed with delivery: an existing transporter instance is currently uploading this package`

Basically, you need to clear out the transport tokens. This can happen if you were to close out of Xcode while in the middle of submitting an app to iTunes Connect.

/Users/<username>/.itmstransporter/UploadTokens/
Delete any .token files in this directory.

https://stackoverflow.com/a/5334320/5684465

---
###Auto kill react-native packager on run-android command
Add these lines to a shell script in your root folder
`lsof -n -i4TCP:8081 | sed '1 d' | awk '{print $2}' | xargs kill -9
react-native run-android`

Add this to your package.json scripts
`"andy": "sh runandy.sh"`

Run with command: `npm run andy`
---

### React Native atob() / btoa() not working without remote JS debugging
https://stackoverflow.com/questions/42829838/react-native-atob-btoa-not-working-without-remote-js-debugging

Here you go (https://sketch.expo.io/BktW0xdje). Create a separate component (e.g. Base64.js), import it and it's ready to use. For instance Base64.btoa('123');

// @flow
// Inspired by: https://github.com/davidchambers/Base64.js/blob/master/base64.js

```
const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=';
const Base64 = {
  btoa: (input:string = '')  => {
    let str = input;
    let output = '';

    for (let block = 0, charCode, i = 0, map = chars;
    str.charAt(i | 0) || (map = '=', i % 1);
    output += map.charAt(63 & block >> 8 - i % 1 * 8)) {

      charCode = str.charCodeAt(i += 3/4);

      if (charCode > 0xFF) {
        throw new Error("'btoa' failed: The string to be encoded contains characters outside of the Latin1 range.");
      }

      block = block << 8 | charCode;
    }

    return output;
  },

  atob: (input:string = '') => {
    let str = input.replace(/=+$/, '');
    let output = '';

    if (str.length % 4 == 1) {
      throw new Error("'atob' failed: The string to be decoded is not correctly encoded.");
    }
    for (let bc = 0, bs = 0, buffer, i = 0;
      buffer = str.charAt(i++);

      ~buffer && (bs = bc % 4 ? bs * 64 + buffer : buffer,
        bc++ % 4) ? output += String.fromCharCode(255 & bs >> (-2 * bc & 6)) : 0
    ) {
      buffer = chars.indexOf(buffer);
    }

    return output;
  }
};

export default Base64;
```


---
### Logging an IOS device on mac
https://stackoverflow.com/questions/7277804/ios-iphone-ipad-ipodtouch-view-real-time-console-log-terminal

```
libimobiledevice is installable via homebrew and works great. Its idevicesyslog tool works similarly to deviceconsole (below), and it supports wirelessly viewing your device's syslog (!)

I've written more about that on Tumblr tl;dr:

brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid>
```

https://github.com/libimobiledevice/libimobiledevice/issues/356#issuecomment-248486535

```
The underlying issue appears to be with the version of libimobiledevice available via homebrew (currently 1.2.0). The simplest workaround until a new release is cut is likely to install from head:

brew uninstall libimobiledevice
brew install --HEAD libimobiledevice
```

---
