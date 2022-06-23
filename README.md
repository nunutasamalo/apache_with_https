# apache_with_https

# generatefreessl

To install 'mod_ssl', run:

  dnf install mod_ssl

To enable the 'mod_ssl' module, run:

 apachectl restart httpd apachectl -M | grep ssl
 
 To allow incoming traffic with HTTPS, run:

firewall-cmd --zone=public --permanent --add-service=https

firewall-cmd --reload

openssl req -newkey rsa:2048 -nodes -keyout /etc/pki/tls/private/httpd.key -x509 -days 365 -out /etc/pki/tls/certs/httpd.crt

Generating a RSA private key
................+++++
..........+++++
writing new private key to '/etc/pki/tls/private/httpd.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:ID
State or Province Name (full name) []: Jakarta
Locality Name (eg, city) [Default City]: Tomang
Organization Name (eg, company) [Default Company Ltd]:Mayora
Organizational Unit Name (eg, section) []:IT
Common Name (eg, your name or your server's hostname) []:registration.clickmayora.local
Email Address []:jairo.manalu@gmail.com

Configure Apache virtual Web-Server with New SSL Certificates
<VirtualHost *:81>
		ServerAdmin www.registration.clickmayora.local
		ServerAlias registration.clickmayora.local
		DocumentRoot /var/www/registration.clickmayora.local/html
		ErrorLog /var/www/registration.clickmayora.local/log/error.log
		CustomLog /var/www/registration.clickmayora.local/log/access.log combined
		SSLEngine on
		SSLCertificateFile /etc/pki/tls/certs/httpd.crt
		SSLCertificateKeyFile /etc/pki/tls/private/httpd.key
</VirtualHost>


Then reload the Apache Web-Server by running:

systemctl reload httpd

Test the 'mod_ssl' configuration

Enter the following in a web browser:

https://your-server-ip or https://your-server-hostname


