# letsencrypt
Setting up Let's Encrypt for Apache on Ubuntu

Tested on Ubuntu 16.04

```
apt install git
mkdir /opt/letsencrypt
git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt

cd /opt/letsencrypt
./letsencrypt-auto --apache -d my.domain.name
```
Answer a couple questions.

Verify on the selected apache configuration file that SSLCertificateFile and SSLCertificateKeyFile are both present and correct.

Set renew of certificate (Let's Encrypt certificates expire in 90 days by default) on crontab:
```
crontab -e
```
add the following row
`15 5 * * 5 /opt/letsencrypt/letsencrypt-auto renew >> /var/log/le-renew.log`

Restart Apache service
```
service apache2 restart
```
done.
