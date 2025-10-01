---
layout: post
title: "svn Not Work After Upgrade to Ubuntu 22.04."
date: 2023-02-21 14:35:00
category: programming
tags: [ubuntu]
---

```
curl -v https://140.122.66.77/svn/personnel_matters/SystemLogAutDo
```

```bash
*   Trying 140.122.66.77:443...
* Connected to 140.122.66.77 (140.122.66.77) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.0 (OUT), TLS header, Certificate Status (22):
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.0 (IN), TLS header, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.2 (OUT), TLS header, Unknown (21):
* TLSv1.3 (OUT), TLS alert, protocol version (582):
* error:0A000102:SSL routines::unsupported protocol
* Closing connection 0
curl: (35) error:0A000102:SSL routines::unsupported protocol
```

如果改了 */usr/lib/ssl/openssl.cnf* 

```bash
[ssl_sect]
system_default = ssl_default_sect

[ssl_default_sect]
MinProtocol = TLSv1		# 不可以是 1.0, 一定只能是 1
CipherString = DEFAULT:@SECLEVEL=1
Options = UnsafeLegacyRenegotiation
```

錯誤訊息就改了:  

```bash
*   Trying 140.122.66.77:443...
* Connected to 140.122.66.77 (140.122.66.77) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* TLSv1.0 (OUT), TLS header, Certificate Status (22):
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.0 (IN), TLS header, Certificate Status (22):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.0 (IN), TLS header, Certificate Status (22):
* TLSv1.0 (IN), TLS handshake, Certificate (11):
* TLSv1.0 (OUT), TLS header, Unknown (21):
* TLSv1.0 (OUT), TLS alert, unknown CA (560):
* SSL certificate problem: self-signed certificate
* Closing connection 0
curl: (60) SSL certificate problem: self-signed certificate
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
```

但是用 svn 去連還是不行,  


就算刪掉 *~/.subversion/auth/svn.ssl.server* 也沒有用:  


### The Working Solution: [Subversion error: svn: E120171: Error running context: An error occurred during SSL communication](https://superuser.com/questions/1473219/subversion-error-svn-e120171-error-running-context-an-error-occurred-during)
最後是先找到 *openssl.conf* 位置:   
```bash
openssl version -d
// /home/linuxbrew/.linuxbrew/etc/openssl@1.1/openssl.cnf
```
然後在檔案頭加入:  

```bash
openssl_conf = default_conf
```

並在檔案最後加入:  

```bash
[ default_conf ]
ssl_conf = ssl_sect

[ssl_sect]
system_default = ssl_default_sect

[ssl_default_sect]
Options = UnsafeLegacyRenegotiation
MinProtocol = TLSv1  
CipherString = DEFAULT:@SECLEVEL=0
```

最重要的, 必須指定這檔案:  

```bash
export OPENSSL_CONF="/home/linuxbrew/.linuxbrew/etc/openssl@1.1/openssl.cnf"
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


