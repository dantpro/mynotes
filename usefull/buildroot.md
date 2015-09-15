# Buildroot

[Buildroot](http://buildroot.uclibc.org/) - это отличный набор Makefile'ов для сборки минималистичных linux-систем на базе uclibc.

Установка очень простая:

```
git clone git://git.buildroot.net/buildroot
# or
git clone http://git.buildroot.net/git/buildroot.git
```

Для настройки последующей сборки и самой сборки:

```
make menuconfig
make
```

Результат сборки потом окажется в `${gitroot}/output`
