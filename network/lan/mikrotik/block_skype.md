# Блокировка Skype

Создаем список ip-адресов серверов skype

```
ip fi ad
add address=111.221.74.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=111.221.77.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=157.55.130.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=157.55.235.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=157.55.56.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=157.56.52.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=194.165.188.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=195.46.253.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=213.199.179.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=63.245.217.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=64.4.23.0/24 comment=disable_skype disabled=no list=skype_servers_z
add address=65.55.223.0/24 comment=disable_skype disabled=no list=skype_servers_z
```

Блокируем все, что в этом списке

```
ip firewall filter
add action=drop chain=forward disabled=no dst-address-list=skype_servers_z
```
