## 修改 nginx.conf 文件

> /etc/nginx/conf.d/nginx.conf

```
server {
  listen 5002;  # 监听的端口（前端通过该端口访问）
  root /home/ma/rag_school/dist;  # 设置静态文件的根目录
  index index.html index.htm;  # 默认文件

  location / {
    try_files $uri $uri/ =404;  # 尝试查找请求的文件，找不到则返回 404
  }

  # Optional: 处理错误页面
  error_page 404 /404.html;
  location = /404.html {
    internal;
  }
  location /api/ {
    proxy_pass http://142.171.108.176:5001;  # 代理到新的后端服务器
    proxy_set_header Host $host;  # 设置 Host 头
    proxy_set_header X-Real-IP $remote_addr;  # 设置客户端真实 IP
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  # 转发客户端 IP
    proxy_set_header X-Forwarded-Proto $scheme;  # 转发协议
  }
}
```

## 修改源码目录权限！

### 1. 查看 nginx 的身份
```bash
ps aux | grep nginx

# www-data 2497744  0.0  0.3  24592  9644 ?        S    00:00   0:00 nginx: worker process
# www-data 2497745  0.0  0.3  24592  9740 ?        S    00:00   0:00 nginx: worker process
```

**确定了身份是 www-data**

然后：

```bash
sudo chown -R www-data:www-data /home/ma/rag_school/dist
sudo chmod +x /home /home/ma /home/ma/rag_school
```