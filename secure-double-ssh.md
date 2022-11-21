# Secure-Double-ssh

Setup highly secure double ssh between two servers both of which are within their respective private networks by bridging over a third server exposed to the public network. <br />
- Target server : target-linux
- Host server : host-linux
- Median Public server : root@linode.thblitz.com
# Steps to set up Double-ssh.

### 1. **ssh to the median server exposed to the public network from the target.**

*``` on the target machine ```*
```sh
ssh -R 8080:localhost:22 root@linode.thblitz.com
```
*``` ssh target -port 22 -> root@linode.thblitz.com -port 8080 ```*

### 2. **ssh to the median server from the host server.**

*``` on the host machine ```*
```sh
ssh -L 8080:localhost:8080 root@linode.thblitz.com
```
*``` ssh host -port 8080 <- root@linode.thblitz.com -port 8080 ```*

### 3. **Finally ssh into the target from the host.**

```sh      
ssh target-linux@localhost -p 8080
```        

### 4. **In case of file transfer via rsync over different ssh port.**

```sh      
rsync --rsh='ssh -p8080' -avP <SourceFolder> target-linux@localhost:/path/to/destination/folder
```
*``` or ```*

```sh
ls /source/folders | xargs -n1 -P4 -I%  rsync --rsh='ssh -p8080' -avzP % target-linux@localhost:/destination/folder
```

