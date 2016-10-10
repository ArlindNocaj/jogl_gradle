# Proguard Problems with JOGL
It seems that proguard breaks the fat jar, even if all the obfuscation/shrinking/optimization is deactivated.
This is a small example showing this problem.

Use gradle to generate the examles:

``` 
gradle proguard
```
 
The generated fat jar is ```build/libs/jogl_gradle-all.jar```. 
This jar is then processed by Proguard leading to ``` build/libs/proguard-jogl_gradle.jar```.

Although the content of the jar files are exactly the same the second one does not work when using:
```
java -jar build/libs/proguard-jogl_gradle.jar
```


# JOGL with Gradle
Sample Gradle project with JOGL.

I did not find it easy to work out how to create a Gradle build for a project utilising JOGL; it was easy to get it to compile, but the native stuffs were never in the right place when in was run.

To get compile to work just depend on the gluegen-rt and jogl-all dependencies:

``` gradle
compile "org.jogamp.gluegen:gluegen-rt:2.3.1"
compile "org.jogamp.jogl:jogl-all:2.3.1"
```

And for the runtime add all the native dependencies:

``` gradle
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-android-aarch64"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-android-armv6"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-linux-amd64"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-linux-armv6"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-linux-armv6hf"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-linux-i586"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-macosx-universal"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-solaris-amd64"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-solaris-i586"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-windows-amd64"
runtime "org.jogamp.gluegen:gluegen-rt:2.3.1:natives-windows-i586"

runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-android-aarch64"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-android-armv6"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-linux-amd64"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-linux-armv6"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-linux-armv6hf"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-linux-i586"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-macosx-universal"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-solaris-amd64"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-solaris-i586"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-windows-amd64"
runtime "org.jogamp.jogl:jogl-all:2.3.1:natives-windows-i586"
```

With this setup you should be able to execute `gradle run` and get a nice window.
