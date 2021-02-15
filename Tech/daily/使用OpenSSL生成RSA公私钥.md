# 使用OpenSSL生成RSA公私钥

1. `openssl genrsa -out rsa_private_key_2048.pem 2048` #生成rsa私钥，X509编码，2048位 

   生成2048位的rsa私钥，默认是X509编码，这一步生成的私钥文件只供第2、3步使用，并没有实际用处

2. `openssl pkcs8 -in rsa_private_key_2048.pem -out rsa_private_key_2048_pkcs8.pem -nocrypt -topk8` #转换为PKCS#8编码 

   使用第1步生成的私钥文件生成PKCS#8编码的私钥文件，这一步生成的文件为最终使用的私钥文件

3. `openssl rsa -in rsa_private_key_2048.pem -out rsa_public_key_2048.pem -pubout` #导出对应的公钥，X509编码

   使用第1步生成的私钥文件生成对应的公钥文件，这一步生成的公钥文件为最终使用的公钥文件