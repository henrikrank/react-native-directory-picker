# react-native-directory-picker
A React Native module that allows you to use native UI to select a directory from the device library

## :warning: What is different in this fork
I had trouble using the library on Android SDK version 28 (Android 9). The app kept crashing after selecting a directory.
I tracked down the issue to missing Android support packages. The import URL for DocumentFile should be updated to 
match the entry in https://developer.android.com/jetpack/androidx/migrate/class-mappings, but I was unable to get 
the library working even after this. As a workaround, I just removed the line using the DocumentFile class.

In my opinion, the DocumentFile class is not needed as it is only used to get a filename from the directory picker, 
which does not make sense, since we are picking directories, not files. 

Feel free to submit an issue or PR if you come up with a more elegant solution. 

###  :warning: Using this component is not recommended. This is a workaround.

## Install

### Android

```bash
$ npm install git+https://github.com/henrikrank/react-native-directory-picker.git
$ react-native link
```

```xml
<!-- file: android/src/main/AndroidManifest.xml -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.myApp">
    <!-- add following permissions -->
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <!-- -->
    ...
```

## Usage
1. In your React Native javascript code, bring in the native module:

  ```javascript
import DirectoryPickerManager from 'react-native-directory-picker';
  ```
2. Use it like so:

  When you want to display the picker:
  ```javascript

  DirectoryPickerManager.showDirectoryPicker(null, (response) => {
    console.log('Response = ', response);

    if (response.didCancel) {
      console.log('User cancelled directory picker');
    }
    else if (response.error) {
      console.log('DirectoryPickerManager Error: ', response.error);
    }
    else {
      this.setState({
        directory: response
      });
    }
  });
  ```

## News
### Compatible with all versions of RN
### Compatible with files from Google Drive
### Requesting permission if not exist
