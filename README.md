# ADS FUCK OFF
<sub>because we all hate them.</sub>

This is a curated list of hosts that will track you, show you ads, spy and some other things.

You will find here the same list in 3 formats:

* [raw list](/hosts/hosts.txt)
* [unbound zone](/unbound/ads.conf)
* [unwind include file](/unwind/ads.conf)

As you probably know I am using #OpenBSD everywhere so I will explain how to make them works over it.

## :.: unbound

```
# cd /var/unbound/etc
# ftp -V https://raw.githubusercontent.com/gonzalo-/ads-fuck-off/main/unbound/ads.conf
...edit unbound.conf and add 'include: "/var/unbound/etc/ads.conf"'...
# /etc/rc.d/unbound restart
```

If your machine is slow, you might want to give unbound service a bit more of timeout by doing:

```
# rcctl set unbound timeout 120
# /etc/rc.d/unbound restart
```

## :.: unwind

Unwind works without any config file, but you can add some magic to it, of course read the manual, but for this purpose a simple config file could be add.

```
# cd /etc
# ftp -V https://raw.githubusercontent.com/gonzalo-/ads-fuck-off/main/unwind/ads.conf
# cat /etc/unwind.conf                                                                                                    
block list "/etc/ads.conf"

fw01="9.9.9.9"
fw02="1.1.1.1"

forwarder { $fw01 $fw02 }

preference { forwarder recursor }
# /etc/rc.d/unwind restart
```
