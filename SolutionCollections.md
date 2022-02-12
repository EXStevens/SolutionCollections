# Solution Collections

(Without any description, solutions have been experimenting on CentOS 8+, Rocky 8) - *2/5/2022*

## Linux Configs

***

### **Change SSH Port**

#### *Fedora*

```Bash
sudo vim /etc/ssh/sshd_config
// #Port 22 -> Port ***

systemctl restart sshd
```

#### *Ubuntu*

```Bash
sudo vim /etc/ssh/sshd_config
// #Port 22 -> Port ***

sudo service ssh restart
```

## Linux Basics

***

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
tar -xf FILE.tar ASSIGNED_FILE (-C OutputDirectory)
```

```Bash
# tar.GZ [-z]
tar -czf FILE.tar.gz FILE
tar -xzf FILE.tar.gz ASSIGNED_FILE (-C OutputDirectory)
```

```Bash
# tar.BZ2 [-j]
tar -cjf FILE.tar.bz2 FILE
tar -xjf FILE.tar.bz2 ASSIGNED_FILE (-C OutputDirectory)
```

```Bash
# tar.XZ [-J]
tar -cJf FILE.tar.xz FILE
tar -xJf FILE.tar.xz ASSIGNED_FILE (-C OutputDirectory)
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

## Install Guides

***

### **PHP 8**

**Use php 8.1.2*

[![Downloads](https://img.shields.io/badge/Downloads-blue "Downloads Page")](https://www.php.net/downloads)

1. **Download the Source**

    Copy the link you need and download and then unzip.

    ```bash
    wget https://www.php.net/distributions/php-8.1.2.tar.gz

    tar -xzf php-8.1.2.tar.gz
    cd php-8.1.2
    ```

1. **Prepare**

    ```bash
    dnf groupinstall "Development Tools"
        
    dnf install libxml2-devel libicu-devel sqlite-devel libxslt-devel libpng-devel libjpeg-devel freetype-devel libzip-devel git
    ```

    Install Oniguruma

    ```bash
    git clone https://github.com/kkos/oniguruma.git
    cd oniguruma
    ./autogen.sh
    ./configure --bindir=/usr/sbin/ \
            --sbindir=/usr/sbin/ \
            --libexecdir=/usr/libexec \
            --sysconfdir=/etc/ \
            --localstatedir=/var \
            --libdir=/usr/lib64/  \
            --includedir=/usr/include/ \
            --datarootdir=/usr/share \
            --infodir=/usr/share/info \
            --localedir=/usr/share/locale \
            --mandir=/usr/share/man/ \
            --docdir=/usr/share/doc/onig
    make && make install
    ```

    Add user for FPM

    ```bash
    adduser www
    ```

1. **Pre-Compile**

    *See all options in [![Option](https://img.shields.io/badge/Offical_Doc-blue)](https://www.php.net/manual/en/configure.about.php#configure.options.misc)*

    **Here are the recommanded options(FPM included):**
    ```bash
    ./configure --prefix=/usr/local/php/ --with-fpm-systemd --with-openssl --enable-bcmath --with-curl --enable-ftp --enable-gd --enable-mbstring --enable-sockets --enable-pcntl --with-zlib --enable-intl --with-fpm-systemd --enable-pdo --enable-xml --with-zip --with-gettext --with-freetype --enable-opcache --enable-shmop
    --with-fpm-user=www --with-fpm-group=www
    ```

    If need to support MySQL, add those options you need. The Directory and Config depend on you env.

    ```bash
    --enable-mysqlnd --with-pdo-mysql=mysqlnd --with-mysqli --with-mysql-sock=/var/lib/mysql/mysql.sock
    ```

1. **Compile & Install**

    ```bash
    make && make install
    ```

### **Nginx-quic**

*The H3 version of Nginx is Experimental.* \
Using it in the Producting Env. is **NOT** recommended.

[![Progress](https://img.shields.io/badge/Progress-blue "Developing Log")](https://hg.nginx.org/nginx-quic/) [![Download](https://img.shields.io/badge/Download_Link-darkgreen "Download Link")](https://hg.nginx.org/nginx-quic/archive/quic.tar.gz)

1. **Prepare**

    ```bash
    dnf groupinstall "Development Tools"
    dnf install openssl openssl-devel
    dnf install curl-devel
    ```

2. **Download & Unzip**

    ```bash
    wget https://hg.nginx.org/nginx-quic/archive/quic.tar.gz
    
    tar -xzf ./quic.tar.gz
    ```
