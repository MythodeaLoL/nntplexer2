# nntplexer

Start your own independant tier 2 usenet business without the need for any storage.

NNTP protocol multiplexer with auth, stats, multiple backends, etc.

1 gbit per vm core, backends are tried in sequential order by priority in case of missing article

## Proxying

### nginx

`nginx.conf`

```nginx
upstream nntplexer {
    least_conn;
    server 127.0.0.1:9999;
}

stream {
    server {
        listen 8888;
        proxy_pass nntplexer;
        proxy_protocol on;
    }
}
```

`nntplexer.ini`

```ini
[server]
proxy_protocol = on
```

![alt text](https://raw.githubusercontent.com/ucrawler/nntplexer/main/grafana%20dashboard.png)
![alt text](https://raw.githubusercontent.com/ucrawler/nntplexer/main/backends%20table.png)
