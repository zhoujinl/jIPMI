# jIPMI Verax IPMI Library

fork from Verax IPMI . And fix some problem

Verax IPMI 默认使用IPMI 2.0 协议，在创建连接的过程中，会首先去获取可用的Cipher Suit。
而有些服务器，并不支持该请求，导致客户端一直停在等待服务器返回的阶段，最终导致任务执行超时 : Command time out.
这是问题1

另外还有一个常见的问题就是，java client 获取到服务端返回的Cipher Suit 后，会随机去获取各种加密算法，例如MD5
但是本身Verax IPMI  默认是没有实现该算法的。

同时参考ipmitool 工具的源码，它并未有此步骤。

因此，综合以上信息，去掉第一步去获取可用的Cipher Suit的操作，直接获取Command: Get Channel Authentication Capabilities (0x38)
可参加具体的包内容

参考使用例子：sample\com\veraxsystems\vxipmi\test

Introduction
====================================================== 
Verax IPMI Library is a Java class package that allows Java applications
to communicate with IPMI v2.0 (Intelligent Platform Management Interface) 
enabled-devices.

Please visit http://www.veraxsystems.com/en/products/ipmilib for the current 
functional specification.


Package contents
====================================================== 
This .zip file contains:
- Pre-built JAR for the library (.\lib directory, just copy to your CLASSPATH and use
  immediately)
- Source code for the library and test drivers (.\src directory)
- JavaDoc documentation (.\doc directory)
- Samples demonstrating how to use the library (.\sample directory)


Prerequisites:
====================================================== 
- Java Development Kit version 1.6 or higher (for compilation):
       * Download from http://www.oracle.com/technetwork/java/javase/downloads/index.html
- Apache Maven 2.2.1 (for building the library, once it's built and added to your
  project it's no longer required):
       * Download http://maven.apache.org/download.cgi
       * Add maven to your path
       * Set JAVA_HOME to point to your JDK e.g.
	     set JAVA_HOME=C:\Program Files\Java\jdk1.7.0_15
         (otherwise maven will not work)


Build instructions (library & test drivers)
====================================================== 
1. Go to ipmilib-x.y.z root directory
2. Run mvn install
3. After successful build you will find library binaries in target directory.
4. In order to build the IPMI library and execute JUnit tests, 
   specify IP address, username and password of the test server
   in src\test\resources\test.properties, set the skipTests parameter in 
   pom.xml to false and run mvn install. 


Importing project to Eclipse
====================================================== 
1. Start Eclipse and select workspace
1. Use: File -> Import -> Existing Maven Projects
2. Select root directory where ipmilib-x.y.z was unpackaged 
3. Once the project is found, click next to add it to the current workspace 


Documentation
====================================================== 
In order to JavaDoc documentation is located in provided along with this package. 
To see it, open doc\index.html in your web browser.


License
====================================================== 
Verax IPMI Library is provided "as is" with no warranty, under GPL version 3.
To see full text of this license go to http://www.gnu.org/copyleft/gpl.html
Please contact us to obtain information on commercial license.



Copyright (c) Verax Systems. All rights reserved.
