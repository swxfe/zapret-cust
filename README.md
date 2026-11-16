##fileplacing

`meta-x.txt:` /opt/zapret/ipset/meta-x.txt

## install dnsmasq cfg

```set -e
for dns in 77.88.8.8 77.88.8.1; do
    rule="/whatsapp.com/static.whatsapp.net/scontent.whatsapp.net/www.instagram.com/$dns"
    uci -q del_list dhcp.@dnsmasq[0].server="/whatsapp.com/www.instagram.com/$dns" || true
    uci -q del_list dhcp.@dnsmasq[0].server="/whatsapp.com/static.whatsapp.net/www.instagram.com/$dns" || true
    uci -q del_list dhcp.@dnsmasq[0].server="$rule" || true
    uci add_list dhcp.@dnsmasq[0].server="$rule"
done
uci commit dhcp
/etc/init.d/dnsmasq restart
```

## uninstall dnsmasq cfg

```set -e
for dns in 77.88.8.8 77.88.8.1; do
    uci -q del_list dhcp.@dnsmasq[0].server="/whatsapp.com/www.instagram.com/$dns" || true
    uci -q del_list dhcp.@dnsmasq[0].server="/whatsapp.com/static.whatsapp.net/www.instagram.com/$dns" || true
    uci -q del_list dhcp.@dnsmasq[0].server="/whatsapp.com/static.whatsapp.net/scontent.whatsapp.net/www.instagram.com/$dns" || true
done
uci commit dhcp
/etc/init.d/dnsmasq restart
```

