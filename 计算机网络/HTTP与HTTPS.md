### **HTTP与HTTPS有什么区别？**

#### **HTTP：**

http是超文本传输协议，信息是明文传输，http的连接是无状态。

####  HTTPS：

  https则是具有安全性的ssl加密传输协议，HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

### Https是如加密的？

#### ①对称加密+非对称加密

1. 某网站拥有用于非对称加密的公钥A、私钥A’。
2. 浏览器像网站服务器请求，服务器把公钥A明文给传输浏览器。
3. 浏览器随机生成一个用于对称加密的密钥X，用公钥A加密后传给服务器。
4. 服务器拿到后用私钥A’解密得到密钥X。
5. 这样双方就都拥有密钥X了，且别人无法知道它。之后双方所有数据都用密钥X加密解密。
#### ②数字证书

网站在使用HTTPS前，需要向“CA机构”申请颁发一份数字证书，数字证书里有证书持有者、证书持有者的公钥等信息，服务器把证书传输给浏览器，浏览器从证书里取公钥就行了。

