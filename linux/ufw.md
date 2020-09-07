Reload Firewall (not always needed)

sudo ufw reload

Open all ports to a specific ip (Should not be done as much as possible)

sudo ufw allow from x.x.x.x

Open specific port to an ip address

sudo ufw allow from x.x.x.x to any port xx

List all UFW rules

sudo ufw status numbered

Delete Rule

sudo ufw delete 1(after numbered view)
