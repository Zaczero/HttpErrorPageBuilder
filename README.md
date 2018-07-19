# HttpErrorPageBuilder

This simple tool generates error pages based on the `template.html` and is configurable with `config.ini`  
You can add your own variables (global or status code scope) which will be visible in generated error page.

[Click here for 404 page demo](https://zaczero.pl/notfound)

## How to build

To generate error pages specified in `config.ini` simply run `build.exe`.  
On the very first run it will fetch status codes details from [https://httpstatuses.com/](https://httpstatuses.com/) and cache them in `cache` directory for later use.

![preview](https://prtsc.me/i/1f99e0c5.jpeg)

## Configuration

We can splig our `config.ini` file into 3 different categories:

### [General]

Here we will configure the build app itself.  
The only variable that you can change in the current version is `codes`.  
`codes` are the status codes for which we are going to generate error pages separated by `,`

#### Example configration
```
[general]
codes=400,401,402,403,404,405,406,407,408,409,410,411,412,413,414,415,416,417,418,421,422,423,424,426,428,429,431,451,500,501,502,503,504,505,506,507,508,510,511,599
```

### [Global]

Here you can define varaibles which will be used for all status codes.

#### Example configration
```
[global]
contact=support@example.com
```

### [Status code]

Here you can define variables which will be used only for one status code.

#### Example configration
```
[404]
title=This file is missing?!
description=We couldn't find this file sir :(
```

## Default variables

`build.exe` defines 3 default variables which are fetched from [https://httpstatuses.com/](https://httpstatuses.com/)

* code
* title
* description

You can see the example usage below.

## Using variables in HTML
```
<p>Status code (numeric): {code}</p>
<p>Status code (title): {title}</p>
<p>Status code's description: {description}</p>
```

### Example output
```
<p>Status code (numeric): 404</p>
<p>Status code (title): Not Found/div>
<p>Status code's description: The origin server did not find a current representation for the target resource or is not willing to disclose that one exists.</p>
```

## Ready to use Nginx configuration
```
error_page 400 /error/400.html;
error_page 401 /error/401.html;
error_page 402 /error/402.html;
error_page 403 /error/403.html;
error_page 404 /error/404.html;
error_page 405 /error/405.html;
error_page 406 /error/406.html;
error_page 407 /error/407.html;
error_page 408 /error/408.html;
error_page 409 /error/409.html;
error_page 410 /error/410.html;
error_page 411 /error/411.html;
error_page 412 /error/412.html;
error_page 413 /error/413.html;
error_page 414 /error/414.html;
error_page 415 /error/415.html;
error_page 416 /error/416.html;
error_page 417 /error/417.html;
error_page 418 /error/418.html;
error_page 421 /error/421.html;
error_page 422 /error/422.html;
error_page 423 /error/423.html;
error_page 424 /error/424.html;
error_page 426 /error/426.html;
error_page 428 /error/428.html;
error_page 429 /error/429.html;
error_page 431 /error/431.html;
error_page 451 /error/451.html;
error_page 500 /error/500.html;
error_page 501 /error/501.html;
error_page 502 /error/502.html;
error_page 503 /error/503.html;
error_page 504 /error/504.html;
error_page 505 /error/505.html;
error_page 506 /error/506.html;
error_page 507 /error/507.html;
error_page 508 /error/508.html;
error_page 510 /error/510.html;
error_page 511 /error/511.html;
error_page 599 /error/599.html;

location ^~ /error/ {
    internal;
    root /var/www;
}
```

Make sure that error pages are imported to `/var/www/error/` directory.  
Example: `/var/www/error/404.html`