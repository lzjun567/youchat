
nginx 配置

```


# 把这段代码配置到server 模块中

#开启openai接口的gzip压缩，大量重复文本的压缩率高，节省服务端流量
gzip  on;
gzip_min_length 1k;
gzip_types text/event-stream;

location ^~ /chatgpt/v1 {

    proxy_pass https://api.openai.com/v1;
    proxy_set_header Host api.openai.com;
	proxy_pass_header Authorization;
	proxy_buffering off;

}
location /chatgpt {
	alias /data/server/chatgpt_gzh/application/templates;
	index chatgpt.html;
}
```

