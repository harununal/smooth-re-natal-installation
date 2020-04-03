```
Date : March 2020
OS : Debian 10
```
---
## Dependencies:
- [Java 8](#java-8)
- [a](#a)


## [Java 8](https://linuxize.com/post/install-java-on-debian-10/)

(If you use :
` sudo apt-get install jdk-default`, you get `jdk11`, but I had some problems on Java11. `java.lang.module.FindException: Module java.xml.bind not found
` etc.)

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

`sudo emacs` or you can use `nano home/<username>/.bashrc`

In emacs : `C-x C-f` `home/<username>/.bashrc`

Add to end of file :
```JAVA_HOME="/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64"```

In emacs : `C-x C-s`

Verify : `echo $JAVA_HOME`
```
Output =>
/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64
```


- [Leiningen](https://leiningen.org/)



- [Android Studio](https://developer.android.com/studio/).

Extract .tar.gz file (my `.tar.gz` downloaded on `Desktop`)

```
~$ cd ~/Desktop
~/Desktop$ tar xvzf  android-studio-ide-xxx-linux.tar.gz
```

Open extracted folder and open a terminal in here

```
~$ cd bin
~bin$ ./studio.sh
```

**Android Studio must be opened.**



---


# baslik-3 
[baslik3](#baslik-3)

See [here](#running-on-linux) for more details.
## Running on Linux
