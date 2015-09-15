# Синхронизация таблиц DNS и DHCP

[Source](http://www.tolaris.com/2014/09/27/synchronising-dhcp-and-dns-on-mikrotik-routers/)

Создаем скрипт со следующим текстом:

```
:local dhcpserver "default"
:local ttl "00:05:00"
:local zone "local"

/ip dns static
:foreach dnsrecord in=[find where name ~ (".*\\.".$zone) ] do={
  :local fqdn [ get $dnsrecord name ]
  :local hostname [ :pick $fqdn 0 ( [ :len $fqdn ] - ( [ :len $zone ] + 1 )) ]
  :local recordttl [get $dnsrecord ttl]
  :if ( $recordttl != $ttl ) do={
    :log debug ("Ignoring DNS record $fqdn with TTL $recordttl")
  } else={
    /ip dhcp-server lease
    :local dhcplease [ find where host-name=$hostname and server=$dhcpserver]
    :if ( [ :len $dhcplease ] > 0) do={
      :log debug ("DHCP lease exists for $hostname, keeping DNS record $fqdn")
    } else={
      :log info ("DHCP lease expired for $hostname, deleting DNS record $fqdn")
      /ip dns static remove $dnsrecord
    }
  }
}

/ip dhcp-server lease
:foreach dhcplease in=[find where server ~ ($dhcpserver)] do={
  :local hostname [ get $dhcplease host-name ]
  :if ( [ :len $hostname ] > 0) do={
    :local dhcpip [ get $dhcplease address ]
    :local fqdn ( $hostname . "." . $zone )
    /ip dns static
    :local dnsrecord [ find where name=$fqdn ]
    :if ( [ :len $dnsrecord ] > 0 ) do={
      :local dnsip [ get $dnsrecord address ]
      :if ( $dnsip = $dhcpip ) do={
        :log debug ("DNS record for $fqdn to $dhcpip is up to date")
      } else={
        :log info ("Updating DNS record for $fqdn to $dhcpip")
        /ip dns static remove $dnsrecord
        /ip dns static add name=$fqdn address=$dhcpip ttl=$ttl
      }
    } else={
      :log info ("Creating DNS record for $fqdn to $dhcpip")
      /ip dns static add name=$fqdn address=$dhcpip ttl=$ttl
    }
  }
}
```
