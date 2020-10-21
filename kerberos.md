## Kerberos setup instructions
```
export NODE=`hostname -f`
export REALM=AMBARI.APACHE.ORG
echo $NODE $REALM
sudo yum -d 1 -y install krb5-server krb5-workstation krb5-libs
sudo sed -i "s/default_realm = EXAMPLE.COM/default_realm = ${REALM}/" /etc/krb5.conf
sudo sed -i "s/EXAMPLE.COM = {/${REALM} = {/" /etc/krb5.conf
sudo sed -i "s/kdc = kerberos.example.com/kdc = ${NODE}/" /etc/krb5.conf
sudo sed -i "s/admin_server = kerberos.example.com/admin_server = ${NODE}/" /etc/krb5.conf
sudo sed -i "/\.example.com = EXAMPLE.COM/d" /etc/krb5.conf
sudo sed -i "s/example.com = EXAMPLE.COM/${NODE} = ${REALM}/" /etc/krb5.conf
printf 'admin\nadmin\n' | sudo kdb5_util create -s -r ${REALM}
sudo sed -i "s/EXAMPLE.COM/${REALM}/" /var/kerberos/krb5kdc/kadm5.acl
sudo kadmin.local -q "addprinc -pw admin admin/admin@${REALM}"
sudo service kadmin start
sudo service krb5kdc start
```
