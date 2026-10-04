server {
    listen 80;
    listen [::]:80;

    server_name _;

    root /var/www/my-web/html;
    index index.html;

    # Khai báo trang lỗi 404 tùy chỉnh
    error_page 404 /404.html;

    location = /404.html {
        root /var/www/my-web/html;
        internal;
    }

    # Cấu hình HTTP Basic Authentication cho khu vực quản trị /admin
    location /admin {
        auth_basic "Restricted Admin Area";
        auth_basic_user_file /etc/nginx/.htpasswd;
        try_files $uri $uri/ =404;
    }

    # Định tuyến mặc định
    location / {
        try_files $uri $uri/ =404;
    }
}