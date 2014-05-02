Docker container for Shopify/dashing

#Interactive
```@bash
docker run --rm -t -i -v /root/hub/dashing-dashboard:/data -p 3030:3030 groob/dashing /sbin/my_init -- bash -l
```

#Daemon
```@bash
docker run -d -v /root/hub/dashing-dashboard:/data -p 3030:3030 groob/dashing /sbin/my_init
```
