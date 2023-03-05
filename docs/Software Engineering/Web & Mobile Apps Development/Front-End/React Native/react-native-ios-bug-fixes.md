# React Native IOS Bug fixes

---

Issue:

To reload the app press "r"
To open developer menu press "d"

2022-09-24T17:17:51,791: [] the permissions on /usr/local/var/run/watchman/freelancing-state allow others to write to it. Verify that you own the contents and then fix its permissions by running `chmod 0700 '/usr/local/var/run/watchman/freelancing-state'`

Watchman: watchman --no-pretty get-sockname returned with exit code=1, signal=null, stderr= 2022-09-24T17:17:51,791: [] the permissions on /usr/local/var/run/watchman/freelancing-state allow others to write to it. Verify that you own the contents and then fix its permissions by running `chmod 0700 '/usr/local/var/run/watchman/freelancing-state'`

OR

What is the meaning of 'No bundle URL present' in react-native?

Solution:

Homebrew Permissions for Watchman on Muti-user Mac

```bash showLineNumbers

sudo chmod 2777 /usr/local/var/run/watchman

sudo rm -rf /usr/local/var/run/watchman/*

```

https://stackoverflow.com/questions/55978254/homebrew-permissions-for-watchman-on-muti-user-mac

---

### react-native-issues-fixed-on-macos

if npm install not working then try to upgrade(if current is old version ) and downgrade. node version (if latest)

**How to install nvm on mac os**

https://tecadmin.net/install-nvm-macos-with-homebrew/
