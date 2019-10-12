# termux-api-package
Termux package containing scripts to call exposed API methods in the [Termux:API](https://github.com/termux/termux-api) app.


In order to allow bluetooth function calls I had to modify the  [shell Termux-API repository](https://github.com/termux/termux-api-package).
So I added two possible shell calls in scripts directory: termux-bluetooth-scaninfo and termux-bluetooth-connect. Both Function calls are similar to the wifi ones since the way to connect is almost the same. However the java functions to be called are different.

I added a BluetoothAPI Class to [Termux:API android-java repository](https://github.com/termux/termux-api) and I modified also the TermuxApiRecivier class in order to make the application call the functions (in BluetoothAPI) to connect and scan.


In the BluetoothAPI class you just have to write the java code to scan bluetooth devices and to connect to them, you can follow the guide in Android Developer official website https://developer.android.com/guide/topics/connectivity/bluetooth. Also you can follow the WifiApi.java file as a guide to create the BluetoothAPi.java

