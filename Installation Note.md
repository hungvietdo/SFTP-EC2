Access to server.

attach volume 50G
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html
Notice: if you want to add a volume with data, the procedure will be slighly different

2. Connect by ssh in macbook or unix
ssh -i "sftp_key.pem" ec2-user@52.89.111.7

Create local key pairs and update to server the public key
https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2
#Install
##update server
`
sudo yum update
`
##Local instalation (putty setup)
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html

##Passive mode installation:
https://www.gosquared.com/blog/fix-ftp-passive-mode-problems-on-amazon-ec2-instances

##Add new sftp group
`
sudo useradd sftp-user
sudo groupadd sftp
sudo usermod -G sftp sftp-user
sudo usermod -d /data sftp-user
`
##Add new sftp user
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/managing-users.html
`
sudo adduser lien
sudo su - lien
mkdir .ssh
chmod 700 .ssh
touch .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
vi .ssh/authorized_keys 
sudo usermod -G sftponly lien
`
##Change user policy
`
sudo vi /etc/ssh/sshd_config
`
###For a group
`
 Match Group sftponly
   ChrootDirectory /data
   ForceCommand internal-sftp
   AllowTcpForwarding no
   PermitTunnel no
   X11Forwarding no
`
###For a user
`Match User username
   ChrootDirectory %h
   ForceCommand internal-sftp
   AllowTcpForwarding no
   PermitTunnel no
   X11Forwarding no
`

sudo service sshd restart


check owner of /data folder
check owner of /data/upload folder

Create local key pairs and update to server the public key
https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2
