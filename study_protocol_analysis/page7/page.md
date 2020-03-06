# 模拟https双向证书验证
```
# CA证书及密钥生成方法一----直接生成CA密钥及其自签名证书
# 如果想以后读取私钥文件ca_rsa_private.pem时不需要输入密码，亦即不对私钥进行加密存储，那么将-passout pass:123456替换成-nodes
openssl req -newkey rsa:2048 -passout pass:123456 -keyout ca_rsa_private.pem -x509 -days 365 -out ca.crt -subj "/C=CN/ST=GD/L=SZ/O=COM/OU=NSP/CN=CA/emailAddress=youremail@qq.com"
# CA证书及密钥生成方法二----分步生成CA密钥及其自签名证书：
# openssl genrsa -aes256 -passout pass:123456 -out ca_rsa_private.pem 2048
# openssl req -new -x509 -days 365 -key ca_rsa_private.pem -passin pass:123456 -out ca.crt -subj "/C=CN/ST=GD/L=SZ/O=COM/OU=NSP/CN=CA/emailAddress=youremail@qq.com"

# 服务器证书及密钥生成方法一----直接生成服务器密钥及待签名证书
# 如果想以后读取私钥文件server_rsa_private.pem时不需要输入密码，亦即不对私钥进行加密存储，那么将-passout pass:server替换成-nodes
openssl req -newkey rsa:2048 -passout pass:server -keyout server_rsa_private.pem  -out server.csr -subj "/C=CN/ST=GD/L=SZ/O=COM/OU=NSP/CN=SERVER/emailAddress=youremail@qq.com"
# 服务器证书及密钥生成方法二----分步生成服务器密钥及待签名证书
# openssl genrsa -aes256 -passout pass:server -out server_rsa_private.pem 2048
# openssl req -new -key server_rsa_private.pem -passin pass:server -out server.csr -subj "/C=CN/ST=GD/L=SZ/O=COM/OU=NSP/CN=SERVER/emailAddress=youremail@qq.com"
# 使用CA证书及密钥对服务器证书进行签名：
openssl x509 -req -days 365 -in server.csr -CA ca.crt -CAkey ca_rsa_private.pem -passin pass:123456 -CAcreateserial -out server.crt
# 将加密的RSA密钥转成未加密的RSA密钥，避免每次读取都要求输入解密密码
# 密码就是生成私钥文件时设置的passout、读取私钥文件时要输入的passin，比如这里要输入“server”
openssl rsa -in server_rsa_private.pem -out server_rsa_private.pem.unsecure

# 客户端证书及密钥生成方法一----直接生成客户端密钥及待签名证书
# 如果想以后读取私钥文件client_rsa_private.pem时不需要输入密码，亦即不对私钥进行加密存储，那么将-passout pass:client替换成-nodes
openssl req -newkey rsa:2048 -passout pass:client -keyout client_rsa_private.pem -out client.csr -subj "/C=CN/ST=GD/L=SZ/O=COM/OU=NSP/CN=CLIENT/emailAddress=youremail@qq.com"
# 客户端证书及密钥生成方法二----分步生成客户端密钥及待签名证书：
# openssl genrsa -aes256 -passout pass:client -out client_rsa_private.pem 2048
# openssl req -new -key client_rsa_private.pem -passin pass:client -out client.csr -subj "/C=CN/ST=GD/L=SZ/O=COM/OU=NSP/CN=CLIENT/emailAddress=youremail@qq.com"
# 使用CA证书及密钥对客户端证书进行签名：
openssl x509 -req -days 365 -in client.csr -CA ca.crt -CAkey ca_rsa_private.pem -passin pass:123456 -CAcreateserial -out client.crt
# 将加密的RSA密钥转成未加密的RSA密钥，避免每次读取都要求输入解密密码
# 密码就是生成私钥文件时设置的passout、读取私钥文件时要输入的passin，比如这里要输入“client”
openssl rsa -in client_rsa_private.pem -out client_rsa_private.pem.unsecure
```
* https://www.cnblogs.com/lsdb/p/9391979.html



