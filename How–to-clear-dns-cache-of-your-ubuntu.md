It can be useful to flush your dns cache. For example if the IP of a domain is changing continously like is the case of an EC2 instance. 

As posted on http://askubuntu.com/questions/414826/how-to-flush-dns-in-ubuntu-12-04 nscd will do the job:
```bash
sudo apt-get install nscd
#Flush DNS Cache in Ubuntu by restarting the nscd
sudo /etc/init.d/nscd restart
```

Of course, if you have the possibility, it can be also a good idea, to just reduce the TTL time of the DNS record.
