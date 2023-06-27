<br />
<p align="center">
  <a href="https://github.com/PecceG2/HTML_Template_http_codes">
    <img src="https://pecceg2.github.io/HTTP_Console_HTML_Template/logo.jpg" alt="Logo" width="100">
  </a>

  <h3 align="center">HTML Templates for HTTP status codes</h3>

  <p align="center">
    HTML Template HTTP Codes is a HTML templates to decorate your HTTP web server responses/errors
	<br />
	Change default nginx/apache templates for a responsive and more attractive design
    <br />
</p>

## Screenshots ##
![Screenshot](https://pecceg2.github.io/HTTP_Console_HTML_Template/readme-banner.png)


## Usage ##
Just clone/download the git repository (The html files are included on error number folder, example "500/index.html" for 500 Internal Server Error)

### NGINX Integration ###

[NGINX](http://nginx.org/en/docs/http/ngx_http_core_module.html#error_page) supports custom error-pages using multiple `error_page` directives.

File: [`nginx.conf`](https://www.nginx.com/resources/wiki/start/topics/examples/full/) (/etc/nginx/)

Example - assumes HttpErrorPages are located into `/usr/share/nginx/html/`.

```nginx
server {
    listen 8000;
    server_name fe;

    try_files $uri $uri/ =404;
    
    # add one directive for each http status code
    error_page 401 /ErrorPages/401/index.html;
    error_page 403 /ErrorPages/403/index.html;
    error_page 404 /ErrorPages/404/index.html;
    error_page 500 /ErrorPages/500/index.html;
    error_page 503 /ErrorPages/503/index.html;
    error_page 504 /ErrorPages/504/index.html;

    # custom location for static files
    location ~* \.(js|jpg|png|css)$ {
        root /usr/share/nginx/html/custom_sources/;
        expires 30d;
    }

    # test error pages    
    location /throw401 {
        return 401;
    }
    location /throw500 {
        return 500;
    }
    location /throw403 {
        return 403;
    }
    location /throw404 {
        return 404;
    }

    location /throw503 {
        return 503;
    }
    location /throw504 {
        return 504;
    }


    # redirect the virtual ErrorPages path the real path
    location /ErrorPages/ {
        alias /usr/share/nginx/html/;
        internal;
    }
}
```

## Apache Httpd Integration ##
[Apache Httpd 2.x](http://httpd.apache.org/) supports custom error-pages using multiple [ErrorDocument](http://httpd.apache.org/docs/2.4/mod/core.html#errordocument) directives.

File: `httpd.conf` or `.htaccess`

Example - assumes HttpErrorPages are located into your **document root** `/var/www/...docroot../ErrorPages`.

```ApacheConf
ErrorDocument 404 /ErrorPages/404/index.html
ErrorDocument 500 /ErrorPages/500/index.html
ErrorDocument 503 /ErrorPages/503/index.html
ErrorDocument 504 /ErrorPages/504/index.html
```

## License
>You can check out the full license [here](https://github.com/PecceG2/HTML_Template_http_codes/blob/master/LICENSE.md)

This project is licensed under the terms of the **MIT** license.