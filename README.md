# nginx unit basic demo project

just for learning unit how to use

## install unit(centos 7)

```bash
nano /etc/yum.repos.d/unit.repo

[unit]
name=unit repo
baseurl=https://packages.nginx.org/unit/centos/$releasever/$basearch/
gpgcheck=0
enabled=1

yum install unit

yum install unit-php unit-python unit-go unit-perl

```

## run demo project

*  start unit server

```bash
systemctl restart unit
```

* application registe

```bash
curl -X PUT -d @$PWD/unit/blog.json  \
       --unix-socket /var/run/control.unit.sock http://localhost/
```

* application describe json file

```json
{
    "listeners": {
        "*:8300": {
            "application": "blogs"
        }
    },

    "applications": {
        "blogs": {
            "type": "php",
            "processes": 20,
            "root": "/opt/blogs/scripts", # where to run 
            "index": "index.php" # index page
        }
    }
}

```

* access

just like below

```bash
curl -i http://localhost:8300
HTTP/1.1 200 OK
X-Powered-By: PHP/5.4.16
Content-type: text/html
Server: Unit/0.7
Date: Sat, 07 Apr 2018 05:00:18 GMT
Transfer-Encoding: chunked
dalong demo unit
```

