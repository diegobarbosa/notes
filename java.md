# Install Java

https://jdk.java.net/

Java SE Development Kit 8u112 on a 64-bit Windows 7 or Windows 8
Set the following user environment variables (== environment variables of type user variables)

- JAVA_HOME : C:\Program Files\Java\jdk1.8.0_112
- JDK_HOME  : %JAVA_HOME%
- JRE_HOME  : %JAVA_HOME%\jre
- CLASSPATH : .;%JAVA_HOME%\lib;%JAVA_HOME%\jre\lib
- PATH      : your-unique-entries;%JAVA_HOME%\bin (make sure that the longish your-unique-entries does not contain any other references to another Java installation folder.

Notice that these environment variables are derived from the "root" environment variable JAVA_HOME. This makes it easy to update your environment variables when updating the JDK. Just point JAVA_HOME to the fresh installation.

java -version
javac -version

http://gedankenverlust.blogspot.de/2012/05/java-environment-variables-definitive.html


## Optional recommendations
- Add an user environment variable JAVA_TOOL_OPTIONS with value -Dfile.encoding="UTF-8". This ensures that Java (and tools such as Maven) will run with a Charset.defaultCharset() of UTF-8 (instead of the default Windows-1252). This has saved a lot of headaches when wirking with my own code and that of others, which unfortunately often assume the (sane) default encoding UTF-8.
- When JDK is installed, it adds to the system environment variable Path an entry C:\ProgramData\Oracle\Java\javapath;. I anecdotally noticed that the links in that directory didn't get updated during an JDK installation update. So it's best to remove C:\ProgramData\Oracle\Java\javapath; from the Path system environment variable in order to have a consistent environment.

source: https://stackoverflow.com/questions/1672281/environment-variables-for-java-installation

Thanks Stack Overflow !!!


## Maven

- Download Maven
- Install in C:\Program Files\Apache\maven
- Add both M2_HOME and MAVEN_HOME variables in the Windows environment, and point it to your Maven folder (C:\Program Files\Apache\maven). 
- Update PATH variable, append Maven bin folder – %M2_HOME%\bin, so that you can run the Maven’s command everywhere.
- Done, to verify it, run mvn –version in the command prompt:

C:\Users\mkyong>mvn -version  
Apache Maven 3.2.2 (45f7c06d68e745d05611f7fd14efb6594181933e; 2014-06-17T21:51:42+08:00)  
Maven home: C:\Program Files\Apache\maven  
Java version: 1.7.0_65, vendor: Oracle Corporation  
Java home: C:\Program Files\Java\jdk1.7.0_65\jre  
Default locale: en_US, platform encoding: Cp1252  
OS name: "windows 8.1", version: "6.3", arch: "amd64", family: "windows"  
C:\Users\mkyong>

*fonte: https://www.mkyong.com/maven/how-to-install-maven-in-windows/

## SPRING Tools Suite

https://spring.io/tools



