openslp-java
============

This is `OpenSLP Java API`, taken from
http://sourceforge.net/projects/openslp/files/OpenSLP-Java/1.0.0/java_slp_api-1.0.tar.gz/download
and made to compile with Java >= 1.5, which just meant renaming all occurences of the variable name `enum` - which is now a keyword, to something else.

# Build and (locally) install to maven, as version 1.0.1 #

```
ant

mvn install:install-file -Dfile=lib/slp.jar -DgroupId=openslp -DartifactId=slp -Dversion=1.0.1 -Dpackaging=jar
```

# Why SLP? #

There's not a lot of information on service discovery without the need for configuration out there. Besides SLP, there is e.g. `SSPD`, which, for this basic and simple task, uses one of the most complex and generic protocols out there - `HTTP`. Another contender is `DNS-SD`, and it is used by Apple, so everyone who pretends to be hip (calm down, I didn't say that every Apple user is necessarily a poser) is using it these days - wittingly or not. I haven't looked to deeply into it, but it does look interesting and might in fact even be technically superior to SLP. Don't know.

# Why openslp-java? #

Why Java (or rather, JVM) library? Because Clojure!

Why openslp-java? Because, in contrast to `jSLP`, I could get it to work with multiple processes registering services on the same box. This is what jSLP gives me:

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
