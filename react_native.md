# React Native Development
===

### Logging an IOS device on mac
https://stackoverflow.com/questions/7277804/ios-iphone-ipad-ipodtouch-view-real-time-console-log-terminal

`libimobiledevice is installable via homebrew and works great. Its idevicesyslog tool works similarly to deviceconsole (below), and it supports wirelessly viewing your device's syslog (!)

I've written more about that on Tumblr tl;dr:

brew install libimobiledevice
idevice_id --list // list available device UDIDs
idevicesyslog -u <device udid>`

`The underlying issue appears to be with the version of libimobiledevice available via homebrew (currently 1.2.0). The simplest workaround until a new release is cut is likely to install from head:

brew uninstall libimobiledevice
brew install --HEAD libimobiledevice`

===
