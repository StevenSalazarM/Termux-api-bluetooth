# termux-api-package
Termux package containing scripts to call exposed API methods in the [Termux:API](https://github.com/termux/termux-api) app. The idea behind this package is to introduce bluetooth commands in the official termux-api-package in order to call methods of a modified version of [Termux:API](https://github.com/termux/termux-api), currently it doesn't work with BLE but it should be possible to introduce BLE inside a java class in [Termux-app-bluetooth](https://github.com/StevenSalazarM/termux-app-bluetooth). The repository just mentioned is a modified version of an old version of the Termux project (**Termux-app-bluetooth is not official**).

In order to allow bluetooth function calls I modified the [shell Termux-API repository](https://github.com/termux/termux-api-package), two possible shell calls were added in *scripts* directory: termux-bluetooth-scaninfo and termux-bluetooth-connect (*ignore termux-enable-buttons*).

The command termux-bluetooth-scaninfo is used to call the functions startDiscovery and cancelDiscovery from the *BluetoothAdapter java class*.

The command termux-bluetooth-connect is used to call a function that has an empty implemetation (for now), you can decide what it should do by introducing your code in the function [onReceiveBluetoothConnect](https://github.com/StevenSalazarM/termux-app-bluetooth/blob/master/app/src/main/java/com/termux/api/BluetoothAPI.java#L106).

An BluetoothAPI class was added in [Termux:API android-java repository](https://github.com/termux/termux-api). Futhermore, TermuxApiReceiver class was modified in order to make the application call the functions to scan and connect.

The implementation of connect is still missing and you can also modify the behaviour of scaninfo by writing your own java code in [BluetoothAPI](https://github.com/StevenSalazarM/termux-app-bluetooth/blob/master/app/src/main/java/com/termux/api/BluetoothAPI.java).


# Usage

### Build and generate the APK

 1) Clone the project in [termux-app-bluetooth](https://github.com/StevenSalazarM/termux-app-bluetooth)
 2) Generate your own apk from the code
 3) Install the apk generated
 4) Open the application and wait for the termux console to be installed (it downloads the binary of termux-api-package available [here](https://github.com/StevenSalazarM/Termux-api-bluetooth/releases/tag/binary3))
 5) Open Termux console by clicking on the button (check *screenshots* directory)
 6) Type *termux-bluetooth-scaninfo* and give the permissions
 7) Type *termux-bluetooth-scaninfo* again to start to scan bluetooth devices
 8) Type *termux-bluetooth-scaninfo* again to stop the scanning (**remember to stop the scanning otherwise a broadcast receiver will stay alive**) and print the results.

### Usage from APK released [here](https://github.com/StevenSalazarM/termux-app-bluetooth/releases/tag/v0.1)

 1) Download termux-app-bluetooth.apk
 2) Install the apk generated (you may need to disable PlayProtect)
 3) Open the application and wait for the termux console to be installed (it downloads the binary of termux-api-package available [here](https://github.com/StevenSalazarM/Termux-api-bluetooth/releases/tag/binary3))
 4) Open Termux console by clicking on the button (check *screenshots* directory)
 5) Type *termux-bluetooth-scaninfo* and give the permissions
 6) Type *termux-bluetooth-scaninfo* again to start to scan bluetooth devices
 7) Type *termux-bluetooth-scaninfo* again to stop the scanning (**remember to stop the scanning otherwise a broadcast receiver will stay alive**) and print the results.

### Contact
If you have any question (or problem) feel free to post it in Issues section or contact me at stevensalazarmolina@gmail.com