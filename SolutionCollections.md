# Solution Collections
(Without any description, solutions have been experimenting on CentOS 8+, Rocky 8) - *2/5/2022*

## Linux Configs

### **Change SSH Port**
####  *Fedora*
```Bash
sudo vim /etc/ssh/sshd_config
// #Port 22 -> Port ***

systemctl restart sshd
```

####  *Ubuntu*
```Bash
sudo vim /etc/ssh/sshd_config
// #Port 22 -> Port ***

sudo service ssh restart
```


## Linux Basics

### **Compression**
#### *Tar* (usually -Action+Format+f)
```Bash
# Query

# List File(s) in the Archive
tar -tf ARCHIVE
# List File(s) in the Archive & Permissions/Owner/Date
tar -tvf ARCHIVE
```
```Bash
# tar
tar -cf FILE.tar FILE
tar -xf FILE.tar <Assigned File> <-C OutputDirectory>(Optional)
```
```Bash
# tar.GZ [-z]
tar -czf FILE.tar.gz FILE
tar -xzf FILE.tar.gz <Assigned File> <-C OutputDirectory>(Optional)
```
```Bash
# tar.BZ2 [-j]
tar -cjf FILE.tar.bz2 FILE
tar -xjf FILE.tar.bz2 <Assigned File> <-C OutputDirectory>(Optional)
```
```Bash
# tar.XZ [-J]
tar -cJf FILE.tar.xz FILE
tar -xJf FILE.tar.xz <Assigned File> <-C OutputDirectory>(Optional)
```
<details>
<summary>Explanation of Parameters</summary>
-c: Create<br>
-x: Decompress<br>
-f: Followed by the files to be processed<br>
-t: Show Content(s) in the archive<br>
-r: Add file(s) to a Tarball<br>
-u: Update files in the archive<br>
-v: Show all progresses<br>
-f: Assign a archive<br>
-C: Jump to an assigned directory<br>
-P: Reserve the properties and permissions<br>
-N: Only save the files newer than DATE-OR-FILE<br>
--exclude=FILE: Exclude FILE<br>
--remove-files: Add and delete
</details><br>

#### *Bzip2*
**If need to RETAIN the Original File(s), add parameter "-k" or "--keep"**
```Bash
bzip2 -ck FILE
bzip2 FILE.bz2
```
#### *Gzip*
**SINGLE FILE ONLY**  
**NOT RETAIN the Original File(s)!**
```Bash
gzip FILE.gz
gunzip FILE.gz
```
#### *Zip*
```Bash
zip FILE.zip FILE
unzip FILE.zip
```


## Installing

### **Nginx-quic**
*The H3 version of Nginx is Experimental.* \
Using it in the Producting Env. is **NOT** recommended.

[![Progress](https://img.shields.io/badge/Progress-blue "Developing Log")](https://hg.nginx.org/nginx-quic/) [![Download](https://img.shields.io/badge/Download-green "Download Link")](https://hg.nginx.org/nginx-quic/archive/quic.tar.gz)

1. Prepare
```bash
dnf groupinstall "Development Tools"
```
2. Download & Unzip
```bash
wget https://hg.nginx.org/nginx-quic/archive/quic.tar.gz

tar -xzf ./quic.tar.gz
```

### **PHP 7**