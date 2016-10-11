# JOGL with Gradle and Proguard
This is a simple example which includes Proguard in the build process.

Note that the ```-keepdirectories``` option is very important for JOGL, otherwise the files cannot be loaded correctly from the output jar and you get the following error:

```
        # A fatal error has been detected by the Java Runtime Environment:
        #
        #  SIGSEGV (0xb) at pc=0x00007fb8fce79b0a, pid=32750, tid=140432495699712
        #
        # JRE version: Java(TM) SE Runtime Environment (8.0_51-b16) (build 1.8.0_51-b16)
        # Java VM: Java HotSpot(TM) 64-Bit Server VM (25.51-b03 mixed mode linux-amd64 compressed oops)
        # Problematic frame:
        # C  [ld-linux-x86-64.so.2+0x9b0a]
        #
        # Core dump written. Default location: /home/user/git/jogl_gradle/core or core.32750
        #
        # An error report file with more information is saved as:
        # /home/user/git/jogl_gradle/hs_err_pid32750.log
        #
        # If you would like to submit a bug report, please visit:
        #   http://bugreport.java.com/bugreport/crash.jsp
        #
```


To run the build process:
``` 
gradle build
```
 
The generated fat jar is ```build/libs/jogl_gradle-all.jar```. 
This jar is then processed by Proguard leading to ``` build/libs/proguard-jogl_gradle.jar```.

Starting the jar starts a window which uses JOGL.
```
java -jar build/libs/proguard-jogl_gradle.jar
```
