First you have to assign dns in
Setting Up MX Records In Your DNS Information
as show in picture

http://123.23.145.23:8081/squirrelmail/src/webmail.php

and need to change the port => if you don't have separate hosted address or port
80 you have to change port no when configuring squirrel mail setup
/etc/apache2/ports.conf =>
change listen to 8081 or whatever

Ref default home page for apache2
https://askubuntu.com/questions/857609/apache2-now-pointing-to-new-default-page
Ref =>
http://www.krizna.com/ubuntu/setup-mail-server-ubuntu-14-04/
Step 6 » Now generate a digital certificate for tls. Issue the commands one by one and provide details as per your domain.

root@saunghayman:~# openssl genrsa -des3 -out server.key 2048
Generating RSA private key, 2048 bit long modulus
....................+++
............+++
e is 65537 (0x10001)
Enter pass phrase for server.key:
Verifying - Enter pass phrase for server.key:
root@saunghayman:~# openssl rsa -in server.key -out server.key.insecure
Enter pass phrase for server.key:
writing RSA key
root@saunghayman:~#  mv server.key server.key.secure
root@saunghayman:~# mv server.key.insecure server.key
root@saunghayman:~#  openssl req -new -key server.key -out server.csr
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:MY
State or Province Name (full name) [Some-State]:Yangoon
Locality Name (eg, city) []:Yangoon
Organization Name (eg, company) [Internet Widgits Pty Ltd]:aung
Organizational Unit Name (eg, section) []:A+
Common Name (e.g. server FQDN or YOUR name) []:saunghayman                                          Email Address []:saunghayman2020.aa@gmail.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:saung
An optional company name []:aung
root@saunghayman:~# openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
Signature ok
subject=/C=MY/ST=Yangoon/L=Yangoon/O=aung/OU=A+/CN=saunghayman/emailAddress=saunghayman2020.aa@gmail.com
Getting Private key