# TP : Proxying avec Squid

## Documentation utilisée

- (https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/configuring-the-squid-caching-proxy-server
- (https://medium.com/@minigear/introduction-to-squid-proxy-server-and-application-5f307245fa1d
- https://wiki.squid-cache.org/SquidFaq/SquidLogs
- https://www.it-connect.fr/mise-en-place-et-configuration-dun-proxy-avec-squid/

## Configuration du serveur Proxy

- Plateforme : AWS
- OS: Debian 11
- Le [Fichier de configuration](./files/squid-config.txt):

Blocage de tous les ports sauf les ports 80, 443 et le port Squid

```bash
acl Safe_ports port 80		# http
acl Safe_ports port 443		# https
acl Safe_ports port 3128	# Squid
acl CONNECT method CONNECT
http_access deny !Safe_ports
```

Port d’écoute client sur 1337:

```bash
http_port 1337
```

Autorisations des sites Epitech et Steam:

```bash
acl whitelist dstdomain .epitech.eu .steampowered.com
http_access allow whitelist
```

Blocage d'une liste de sites:

- Dans le fichier de configuration Squid:

```bash
acl domain_blacklist dstdomain "/etc/squid/domain_blacklist.txt"
http_access deny all domain_blacklist
```

- Dans la blocklist `/etc/squid/domain_blacklist.txt`:

```bash
.ynov.com
.microsoft.com
.leagueoflegends.com
```

## Configuration du proxy sur le navigateur

![Configuration Firefox](./files/ConfigFireFox.png)
Afin d'appliquer le proxy sur le navigteur, il faudra se rendre dans les paramètres de Firefox:
Général > _Network Settings_ > Séléctionner _Manual proxy configuration_.

![Accès Refusé](./files/AccessDenied.png)

(WIP)
