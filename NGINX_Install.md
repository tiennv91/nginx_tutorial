## Choosing Between a Stable or a Mainline Version
NGINX Open Source is available in two versions:

- The mainline version. This version includes the latest features and bugfixes and is always up-to-date. It is reliable, but it may include some experimental modules, and it may also have some number of new bugs.
- The stable version. This version doesn’t have new features, but includes critical bug fixes that are always backported to the mainline version. The stable version is recommended for production servers.

## Choosing Between a Pre-built Package or Compiling From the Sources
Both NGINX Open Source mainline and stable versions can be installed in two ways:

- from a pre-built package. This is a quick and easy way to install NGINX Open Source. The package includes almost all NGINX official modules and is available for most popular operating systems.
- compiled from the sources. This way is more flexible: you can add particular modules including 3rd party modules or apply latest security patches.

## Compiling and Installing From the Sources
### Installing NGINX Dependencies
- the PCRE library – required by NGINX Core and Rewrite modules and provides support for regular expressions:

```
$ wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.40.tar.gz
$ tar -zxf pcre-8.40.tar.gz
$ cd pcre-8.40
$ ./configure
$ make
$ sudo make install
```
- the zlib library – required by NGINX Gzip module for headers compression:
```
$ wget http://zlib.net/zlib-1.2.11.tar.gz
$ tar -zxf zlib-1.2.11.tar.gz
$ cd zlib-1.2.11
$ ./configure
$ make
$ sudo make install
```
- the OpenSSL library – required by NGINX SSL modules to support the HTTPS protocol:
```
$ wget http://www.openssl.org/source/openssl-1.0.2f.tar.gz
$ tar -zxf openssl-1.0.2f.tar.gz
$ cd openssl-1.0.2f
$ ./config --prefix=/usr --openssldir=/etc/ssl --libdir=lib no-shared zlib-dynamic
$ make
$ sudo make install
```

### Download source and compiling
**Download source**

To download and unpack source files for the latest mainline version, type-in the commands:
```
$ wget http://nginx.org/download/nginx-1.11.13.tar.gz
$ tar zxf nginx-1.11.13.tar.gz
$ cd nginx-1.11.13
```
To download and unpack source files for the latest stable version, type-in the commands:
```
$ wget http://nginx.org/download/nginx-1.12.0.tar.gz
$ tar zxf nginx-1.12.0.tar.gz
$ cd nginx-1.12.0
```

**Configuring the Build Options**

```
$ ./configure --sbin-path=/usr/local/nginx/nginx --conf-path=/usr/local/nginx/nginx.conf --pid-path=/usr/local/nginx/nginx.pid --with-http_ssl_module --with-stream --with-pcre=../pcre-8.40 --with-zlib=../zlib-1.2.11 --without-http_empty_gif_module
```

**Compile and install the build:**
```
$ make
$ sudo make install
```

**After the installation is finished, run NGINX Open Source:**
```
$ sudo nginx
```
_**Note:**_ If you have received a message: `nginx: command not found`. Please add this code in `~/.bashrc` and run `source ~/.bashrc`.
```
export PATH=$PATH:/usr/local/nginx
```

## Installing a Pre-Built Package
References: https://www.nginx.com/resources/admin-guide/installing-nginx-open-source/
### Installing Red Hat/CentOS Packages
#### Installing NGINX package From a Default Red Hat/CentOS Repository
```
$ sudo yum install epel-release
$ sudo yum update
$ sudo nginx -v
#  nginx version: nginx/1.6.3
```
#### Installing From NGINX Repository
```
$ sudo vi /etc/yum.repos.d/nginx.repo
```
Add this line to the file
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/OS/OSRELEASE/$basearch/
gpgcheck=0
enabled=1
```
