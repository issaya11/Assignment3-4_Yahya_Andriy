#below is the code that we inserted to fix this vulnerability

server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /code;

    index index.php; 

    server_name 0.0.0.0;
    charset utf-8;

    location ~ .php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+.php)(/.+)$;
        fastcgi_pass php:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
}
