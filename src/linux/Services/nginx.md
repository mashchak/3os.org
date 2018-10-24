title: Linux - Nginx
description: Linux - Nginx how to, guides, examples, and simple usage

# Nginx

## Show all domains in NGINX configuration

```bash
grep -e "^\s*server_name" /etc/nginx/conf.d/*|sed -e 's/[\t ]*server_name//g;'|sed -e "s/ /\+/g"|sed -e 's/;//g'|while read line; do for i in $line; do echo -n "$i "|sed -e 's/://'  -e 's/\+/\n  |--/g'; done ;echo; done; echo
```

## Engintron generate custom_rules for all domains on the server

```bash
ip=`hostname -i` && for domain in `httpd -S |  grep www. | awk -F 'www.' '{print $2}'`;do printf "if ( \$host ~ \"%s\") {set \$PROXY_DOMAIN_OR_IP \"$ip\";}\n" $domain ;done >> /etc/nginx/custom_rules && service nginx reload
```

<!-- Donation Button -->
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" align="center"><input type="hidden" name="cmd" value="_s-xclick"><input type="hidden" name="hosted_button_id" value="Q94AU5RUD4X6A"><input type="image" src="https://raw.githubusercontent.com/fire1ce/3os.org/gh-pages/assets/images/beerDonation.png" width="220px" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!"><img alt="" border="0" src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" width="1" height="1"></form>
<!-- Donation Button -->