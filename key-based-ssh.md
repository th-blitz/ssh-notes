# key-based-ssh-authentication

Setup public-key based authentication in ssh. <br />

# Steps to set up key-based authentication.

### 1. **Create a key pair: the keys must be named as ~/.ssh/id_rsa.**

```sh
ssh-keygen
```

### 2. **Copying the public key (id_rsa.pub) from local host -> to the remote machine.**

```sh
cat ~/.ssh/id-rsa.pub | ssh *username@remote_host* "mkdir -p ~/.ssh && cat >> ~/.shh/authorized_keys"
```
*``` copying using ssh ```*

```sh
cat ~/.ssh/id_rsa.pub
```
```sh
echo *public_key_string* >> ~/.ssh/authorized_keys
```
*``` copying manually ```*

### 3. **Authenticate with the remote machine**

```sh      
ssh *username@remote_host* 
```        

### 4. **Disable password based authentication**

```sh      
sudo vim /etc/ssh/sshd_config
```
*```set password authentication to no```*
```sh
PasswordAuthentication no
```

### 5. **Restart sshd server**

```sh      
sudo service sshd restart
```        
