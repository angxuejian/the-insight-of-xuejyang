# Nginx

## Install

```bash
sudo apt update
sudo apt install nginx
```

<details>
    <summary>Example</summary>

```bash
# /etc/nginx/nginx.conf
# /etc/nginx/conf.d

# sudo cp test-project/nginx.conf /etc/nginx/conf.d/test.conf

# sudo ln -s \$(pwd)/test-project/nginx.conf \/etc/nginx/conf.d/test.conf

```

</details>

## Commands
| 命令                      | 作用         |
| ----------------------- | ---------- |
| nginx                   | 启动 nginx   |
| nginx -s stop           | 立即停止       |
| nginx -s quit           | 优雅关闭       |
| nginx -s reload         | 重载配置（最常用）  |
| nginx -t                | 检查配置文件是否正确 |
| systemctl start nginx   | 启动服务       |
| systemctl stop nginx    | 停止服务       |
| systemctl restart nginx | 重启         |
| systemctl status nginx  | 查看状态       |
| systemctl enable nginx  | 开机自启       |
