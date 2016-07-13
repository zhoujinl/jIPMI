# jIPMI Verax IPMI Library

fork from Verax IPMI . And fix some problem.

Verax IPMI 默认使用IPMI 2.0 协议，在创建连接的过程中，会首先去获取可用的Cipher Suit。
而有些服务器，并不支持该请求，导致客户端一直停在等待服务器返回的阶段，最终导致任务执行超时 : Command time out.
这是问题1

另外还有一个常见的问题就是，java client 获取到服务端返回的Cipher Suit 后，会随机去获取各种加密算法，例如MD5
但是本身Verax IPMI  默认是没有实现该算法的。

同时参考ipmitool 工具的源码，它并未有此步骤。

因此，综合以上信息，去掉第一步去获取可用的Cipher Suit的操作，直接获取Command: Get Channel Authentication Capabilities (0x38)
可参加具体的包内容。

参考使用例子：sample\com\veraxsystems\vxipmi\test
对于使用者来说，跟原先的区别只是在openSession之前，之后的步骤都是一样的。



Copyright (c) Verax Systems. All rights reserved.
