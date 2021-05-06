# kubernetes-cluster-build
## Preparation

Execute the below commands before using the scripts in the repo.
```
yum install epel-release -y
yum install git unzip wget ansible -y
git clone -b develop https://github.com/aruntony005/kubernetes-cluster-build-ansible.git
mkdir /root/.ssh
gpg --quiet --batch --yes --decrypt --passphrase="aruntony" --output /root/.ssh/authorized_keys /root/kubernetes-cluster-build-ansible/public_key.gpg
gpg --quiet --batch --yes --decrypt --passphrase="aruntony" --output /root/.ssh/id_rsa /root/kubernetes-cluster-build-ansible/private_key.gpg
sudo sed -i '/PasswordAuthentication/d;/PermitRootLogin/d;/PubkeyAuthentication/d' /etc/ssh/sshd_config
sudo chmod 700 /root/.ssh
sudo chmod 600 /root/.ssh/id_rsa
sudo chmod 644 /root/.ssh/authorized_keys
sudo echo -e "PermitRootLogin yes\nPubkeyAuthentication yes\nPasswordAuthentication yes" >> /etc/ssh/sshd_config
sudo systemctl restart sshd
```

The keys and secrets in this repos are encrypted using gpg.
```
gpg --symmetric --cipher-algo AES256 file_name

gpg --quiet --batch --yes --decrypt --passphrase="$SECRET_PASSPHRASE" --output $HOME/secrets/my_secret.json my_secret.json.gpg
```

