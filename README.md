# termux-api-package
Termux package containing scripts to call exposed API methods in the [Termux:API](https://github.com/termux/termux-api) app. The idea behind this package is to introduce bluetooth commands in the official termux-api-package in order to call methods of a modified version of [Termux:API](https://github.com/termux/termux-api), you can find two java classes BluetoothAPI and BluetoothLowEnergyAPI (this one under the branch dev-ble) in [Termux-app-bluetooth](https://github.com/StevenSalazarM/termux-app-bluetooth). The repository just mentioned is a modified version of an old version of the Termux project (**Termux-app-bluetooth is not official**).

In order to allow bluetooth function calls I modified the [shell Termux-API repository](https://github.com/termux/termux-api-package), two possible shell calls were added in *scripts* directory: termux-bluetooth-scaninfo and termux-bluetooth-connect (*ignore termux-enable-buttons*).

The command termux-bluetooth-scaninfo is used to call the functions startDiscovery and cancelDiscovery from the *BluetoothAdapter java class*.

The command termux-bluetooth-connect is used to call a function that has an empty implemetation (for now), you can decide what it should do by introducing your code in the function [onReceiveBluetoothConnect](https://github.com/StevenSalazarM/termux-app-bluetooth/blob/master/app/src/main/java/com/termux/api/BluetoothAPI.java#L106).

A BluetoothAPI class was added in [Termux:API android-java repository](https://github.com/termux/termux-api). Futhermore, TermuxApiReceiver class was modified in order to make the application call the functions to scan and connect.

The implementation of connect is still missing and you can also modify the behaviour of scaninfo by writing your own java code in [BluetoothAPI](https://github.com/StevenSalazarM/termux-app-bluetooth/blob/master/app/src/main/java/com/termux/api/BluetoothAPI.java).

In addition to the BluetoothAPI class it was introduced also another class [BluetoothLowEnergyAPI](https://github.com/StevenSalazarM/termux-app-bluetooth/blob/dev-ble/app/src/main/java/com/termux/api/BluetoothLowEnergyAPI.java). This class is under the dev-ble branch and it hasnt been merged to master due to the lack of bluetooth low enegery devices for testing. 

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

### Usage example
At the moment it shows only devices name but you can [add more info](https://github.com/StevenSalazarM/termux-app-bluetooth/blob/master/app/src/main/java/com/termux/api/BluetoothAPI.java#L36) to be printed.

<p align="center"><img src="https://github.com/StevenSalazarM/Termux-api-bluetooth/blob/master/screenshots/termux-bluetooth-scaninfo-release.jpeg"  height="50%" width="25%" ></p>

### Possible Problem
If you are getting message below probably you used a command inside termux console that required to update or install a package.
```sh
E: This installation run will require temporarily removing the essential package libandroid-support:aarch64 due to a Conflicts/Pre-Depends loop. This is often bad, but if you really want to do it, activate the APT::Force-LoopBreak option.
E: Internal Error, Could not early remove libandroid-support:aarch64 (2)
```
The reason of the problem can be found in  [Termux-Package issue 4129](https://github.com/termux/termux-packages/issues/4129#issuecomment-519487869).

>Hmm, there happens following:
   >- Few months ago iconv() implementation was moved from libandroid-support to libiconv. But since old libandroid-support provides libiconv.so symlink used by essential utilities (like coreutils), package libiconv can't be installed.
   >- Now busybox was replaced by separate packages which makes coreutils to be required for installation. So here a conflict loop starts to happen.

Thus, since the apk in [Termux-app-bluetooth](https://github.com/StevenSalazarM/termux-app-bluetooth) is based on the version 0.64 of the Termux project you must install a more recent version of it. 

_However, after September, I will try to work on a new version of Termux-app-bluetooth that supports update or installation of packages._

### Contact
If you have any question (or problem) feel free to post it in Issues section or contact me at stevensalazarmolina@gmail.com
