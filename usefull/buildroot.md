# Buildroot

[Buildroot](http://buildroot.uclibc.org/) - это отличный набор Makefile'ов для сборки минималистичных linux-систем на базе uclibc.

Установка очень простая:

```sh
git clone git://git.buildroot.net/buildroot
# or
git clone http://git.buildroot.net/git/buildroot.git
```

Для настройки последующей сборки и самой сборки:

```sh
make menuconfig
make
```

Результат сборки потом окажется в `${gitroot}/output`
