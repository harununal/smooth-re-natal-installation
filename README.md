```
Date : March 2020
OS : Debian 10
```
---
## Dependencies:
- [Java 8](#java-8)
- [Leiningen](#leiningen)
- [nvm](#nvm)
- [re-natal and react-native](#re-natal-and-react-native)
- [Android Studio](#android-studio)



---

## [Java 8](https://linuxize.com/post/install-java-on-debian-10/)

If you use :
` sudo apt-get install jdk-default`

you get `jdk11`

but I had [some problems](https://stackoverflow.com/questions/58495573/module-java-xml-bind-not-found) on Java11 
```
For example =>
java.lang.module.FindException: Module java.xml.bind not found
```

  **Install jdk8 [*](https://linuxize.com/post/install-java-on-debian-10/) :**

```
sudo apt update
sudo apt install apt-transport-https ca-certificates wget dirmngr gnupg software-properties-common
```
```
wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | sudo apt-key add -
```
```
sudo add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
```
```
sudo apt update
sudo apt install adoptopenjdk-8-hotspot
```
```
java -version
```
```
OUTPUT =>
openjdk version "1.8.0_212"
OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.212-b04, mixed mode)
``` 
*If you have emacs :*

`sudo emacs` 

(or you can use `nano home/<username>/.bashrc`)

In emacs : `C-x C-f` (find file) `home/<username>/.bashrc`

Add to end of file :
```JAVA_HOME="/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64"```

In emacs : `C-x C-s` (save)

Verify : `echo $JAVA_HOME`
```
Output =>
/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64
```
---

## [Leiningen](https://leiningen.org/)
```
sudo apt-get install -y leiningen
```
Check java version. Leiningen brings java11 :

```
sudo update-alternatives --config java
```
```
Output =>
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                                Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java          1111      auto mode
  1            /usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/bin/java   1081      manual mode
  2            /usr/lib/jvm/java-11-openjdk-amd64/bin/java          1111      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```
Press `1` `Enter`
```
Output =>
update-alternatives: using /usr/lib/jvm/adoptopenjdk-8-hotspot-amd64/bin/java to provide /usr/bin/java (java) in manual mode
```
Verify : `lein -version`
```
Output =>
Leiningen 2.9.0 on Java 1.8.0_242 OpenJDK 64-Bit Server VM
```
---

## [nvm](https://github.com/nvm-sh/nvm)

(for installing nodejs.v8.xx)

If you use:
```
sudo apt install nodejs
```
you get `nodejs v10.xx`


but I had some problems on v10 like that in [this page](https://github.com/nodejs/help/issues/1877):
```
1 warn npm npm does not support Node.js v10.15.2
2 warn npm You should probably upgrade to a newer version of node as we
3 warn npm can't make any promises that npm will work with this version.
4 warn npm Supported releases of Node.js are the latest release of 4, 6, 7, 8, 9.
```

**Install nvm [*](https://github.com/nvm-sh/nvm)**
```
sudo apt-get install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
```
nvm ls
```
```
Output =>
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.17.1 (-> N/A)
lts/carbon -> v8.17.0
lts/dubnium -> v10.19.0 (-> N/A)
lts/erbium -> v12.16.1 (-> N/A)
```
```
nvm install v8.17.0
nvm use v8.17.0 
```
Verify : `npm --version` => 6.13.4
`node --version` => v8.17.0

---
## [re-natal and react-native](http://anish-patil.blogspot.com/2019/02/how-to-create-react-native-project-with.html)
```
npm install -g react-native-cli
npm install -g re-natal
re-natal init <aCamelCaseNamedProject>
```
```
cd a-camel-case-named-project; yarn
```
---

## [Android Studio](https://developer.android.com/studio/)

Download [Android Studio](https://developer.android.com/studio/)

Extract `.tar.gz` file (my `.tar.gz` downloaded on `Desktop`)

```
~$ cd ~/Desktop
~/Desktop$ tar xvzf  android-studio-ide-xxx-linux.tar.gz
```

Open extracted folder and open a terminal in here

```
~$ cd bin
~bin$ ./studio.sh
```

**Android Studio must be opened now.**

---

[Set SDK](https://medium.com/@loons.create/2-react-native-tutorial-android-studio-android-sdk-6a630b7ed517)

On `Start a new Android project` page :
`Configure` > `SDK Manager` > `Android SDK`

`SDK Platforms` > Select SDK that you want

Check the box : `Show Package Details`

and check this three box
```
- Android SDK Platform XXX
- Intel x86 Atom_64 System Image
- Google APIs Intel x86 Atom System Image
```
`Apply`

---
**Setting HOME_ANDROID**

Open `.bashrc`

Add to end :

```
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```
Check :

`echo $ANDROID_HOME`

---

**Emulator**

`Open an existing Android Studio project` => Your project file : `a-camel-case-named-project`

`Avd Manager` (a symbol on right-top, like phone screen)

`Create Virtual Drive` => `Nexus5` or anything => `Double-click`

---
### Extra Settings for Android Studio :

[Increase the watches limit](https://confluence.jetbrains.com/display/IDEADEV/Inotify+Watches+Limit)

Create a `x.conf` file in `/etc/sysctl.d/` (I used emacs again)

Add a line in this file : 
 
`fs.inotify.max_user_watches = 524288`

`Save`

`sudo sysctl -p --system`

**restart Android Studio**

---

## Everything is ready, let's cook !

Open first terminal in project folder

```
re-natal use-android-device avd
re-natal use-figwheel
lein figwheel android
```

Open second terminal in project folder

`react-native run-android`

**You must have Hello Clojure in IOS and Android screen in emulator.**

Change your project with an editor :
- Emacs/cider
- Visual Studio Code/calva
- etc.

**Enjoy with Clojurescript !**

---

#### Sources :
- [http://anish-patil.blogspot.com/2019/02/how-to-create-react-native-project-with.html](http://anish-patil.blogspot.com/2019/02/how-to-create-react-native-project-with.html)
- [https://linuxize.com/post/install-java-on-debian-10/](https://linuxize.com/post/install-java-on-debian-10/)
- [https://github.com/nodejs/help/issues/1877](https://github.com/nodejs/help/issues/1877)
- [https://github.com/bhauman/lein-figwheel](https://github.com/bhauman/lein-figwheel)
- [https://cljsrn.org/](https://cljsrn.org/)
- [https://github.com/drapanjanas/re-natal](https://github.com/drapanjanas/re-natal)
- [https://confluence.jetbrains.com/display/IDEADEV/Inotify+Watches+Limit](https://confluence.jetbrains.com/display/IDEADEV/Inotify+Watches+Limit)
- [https://medium.com/@loons.create/2-react-native-tutorial-android-studio-android-sdk-6a630b7ed517](https://medium.com/@loons.create/2-react-native-tutorial-android-studio-android-sdk-6a630b7ed517)
- [https://stackoverflow.com/questions/58495573/module-java-xml-bind-not-found](https://stackoverflow.com/questions/58495573/module-java-xml-bind-not-found)
