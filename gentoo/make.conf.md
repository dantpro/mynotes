# make.conf

This is my make.conf for server installations of gentoo. Because of sometimes I have few packages patched (right now it is nginx with http2 support), it could make some failures, however, I hope these patches will go to stable tree soon.

```sh
CFLAGS="-Os -pipe -march=native"
CXXFLAGS="${CFLAGS}"
CHOST="x86_64-pc-linux-gnu"
USE="bindist mmx sse sse2 vim-syntax gnutls http2 -X -ipv6 -nls -gtk -qt -qt4 -doc -webdav -acl"

PORTDIR="/usr/portage"
DISTDIR="${PORTDIR}/distfiles"
PKGDIR="${PORTDIR}/packages"

# Change it to your cores count +1.
MAKEOPTS="-j1"

EMERGE_DEFAULT_OPTS="-av --quiet-build y"

# If you don't reed manpages on server, you could add 'noman' here
FEATURES="nodoc noinfo"

LINGUAS="en"
AUTOCLEAN="yes"

GENTOO_MIRRORS="http://mirror.yandex.ru/gentoo-distfiles/
    http://mirror2.corbina.ru/gentoo-distfiles/
    http://gentoo.inode.at/
    http://de-mirror.org/gentoo/
    "

NGINX_MODULES_HTTP="access auth_basic autoindex browser charset empty_gif fastcgi geo gzip limit_conn limit_req map proxy referer rewrite split_clients ssi upstream_ip_hash userid http2 geoip gunzip gzip_static realip headers_more"
PHP_TARGETS="php5-6"
```
