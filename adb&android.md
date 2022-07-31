### List packages
- List system packages:
```
adb shell 'pm list packages -f'
```
- List 3rd party packages:
```
adb shell 'pm list packages -3 -f'
```
-  Pull apk `adb pull /data/app/<package_name/base.apk>`

### SSL Pinning bypass
1. Using pcap and modifying apk  `https://www.exandroid.dev/2021/03/21/capture-all-android-network-traffic/`

### BLogs
1. https://blog.oversecured.com

### Frida
1. ADB root
2. Push cacert (adb push 9a5ba575.0 /system/etc/security/cacerts/)
	1. If (remote couldn't create file: Read-only file system)
	2. Simply remount as rw (Read/Write):
	```bash
	# mount -o rw,remount /system
	```
	Once you are done making changes, remount to ro (read-only):
	```bash
	# mount -o ro,remount /system
	```
### Nuclei templates
https://gist.github.com/rudSarkar/8d4ae6f2d222020d1f45885650f941ab
https://github.com/optiv/mobile-nuclei-templates