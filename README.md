openslp-java
============

This is basically just a copy of `OpenSLP Java API`, as taken from
http://sourceforge.net/projects/openslp/files/OpenSLP-Java/1.0.0/java_slp_api-1.0.tar.gz/download

Differences to original:

* made it compile with Java >= 1.5, which just meant renaming all occurences of the variable name `enum` to something else
* mavenized (quick and dirty) so we can e.g. `mvn install` it. A simple `mvn install:install-file` of the jar file created by ant would not have done the trick, as we need to specify the dependency on `log4j`

Please check the original license in `license.txt` if you want to use the library.

# Why SLP? #

There is not a lot of information out there on configuration-less service discovery. Besides SLP, there is `SSPD`, which, for this basic and simple task, uses one of the most complex and generic protocols out there - `HTTP`. I decided to stop onvestigating that one right there.

Another contender is `DNS-SD`, and it is used by Apple, so everyone who pretends to be hip (calm down, I didn't say that every Apple user is *necessarily* a poser) is using it these days - wittingly or not. I haven't investigated it too deeply either, but it does look interesting and might in fact even be technically superior to SLP. Don't know.

# Why openslp-java? #

Why a Java (or rather, JVM) library? Because it can be easily used from great languages such as clojure.

Why openslp-java? Because in contrast to `jSLP`, I could get it to work with multiple processes registering services on the same box. This is what jSLP gives me instead:

```
[ERROR] SLPCore - Exception: <java.net.SocketTimeoutException: Receive timed out>java.net.SocketTimeoutException: Receive timed out
        at java.net.PlainDatagramSocketImpl.receive0(Native Method)
        at java.net.AbstractPlainDatagramSocketImpl.receive(AbstractPlainDatagramSocketImpl.java:145)
        at java.net.DatagramSocket.receive(DatagramSocket.java:786)
        at ch.ethz.iks.slp.impl.SLPCore.sendMessage(SLPCore.java:729)
        at ch.ethz.iks.slp.impl.AdvertiserImpl.register(AdvertiserImpl.java:135)
        at clojure_jslp.core$register_service.invoke(core.clj:31)
```

Also, it is easy to use openslp-java on the standard port 427 - assuming you are running `slpd`. `jSLP` needs to run as root to be able to listen on 427.
