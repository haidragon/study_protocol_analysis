# openssl编译与使用
## [openssl  编译](https://wiki.openssl.org/index.php/Compilation_and_Installation#OS_X)
生成密钥对
web交换
客户端验证服务器
客户端把数据用自己的私钥加密然后把自己的公钥与加密的数据去ca用ca私钥加密发给服务器
服务器拿到数据去ca用公钥解密拿到客户端的真正公钥同时用客户端公钥解密把数据发给客户端
客户端对比数据

服务器验证客户端
服务器把数据用自己的私钥加密然后把自己的公钥与加密的数据去ca用ca私钥加密发给客户端
客户端拿到数据去ca用公钥解密拿到服务器的真正公钥同时用服务器公钥解密把数据发给服务器
服务器对比数据






* https://github.com/danielctull/openssl-xcode 
* http://blog.chinaunix.net/uid/26729093/cid-198661-list-1.html
* https://www.jianshu.com/p/15b1d935a44b
* https://www.cnblogs.com/LiuYanYGZ/p/10405532.html
* https://www.jianshu.com/p/3c5212b47bec


