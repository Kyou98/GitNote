# Curl Notes:
Refer to: <https://bagder.gitbook.io/everything-curl/cmdline>
## Install in MaxOS
```
brew install curl
```
---
## Common line basics
 -K common-line options through a file or from stdin(standard input)

```
curl -K
```
switch on verbose mode(with detail info) with the -v option:
```
curl -v https://example.com
```
or
```
curl -verbose https://example.com
```
The command-line parser in curl always parses the entire line and you can put the options anywhere you like; they can also appear after the URL:
```
curl  https://example.com -Lv
```
and the two separate short options can of course also be specified separately, like:
```
curl -v -L https://example.com
```
or
```
curl -verbose -location https://example.com
```
FTP
```
curl ftp://ftp.example.com/README
```
with user and password
```
curl ftp://user:password@example.com/
```
HTTP\
with user and password
```
$ curl -u alice:12345 http://example.com/
```
---
## Arguments to options
Not all options are just simple boolean flags that enable or disable features. For some of them you need to pass on data, like perhaps a user name or a path to a file. You do this by writing first the option and then the argument, separated with a space. Like, for example, if you want to send an arbitrary string of data in an HTTP POST to a server:
```
curl -d arguments http://example.com
```
When use the short options with arguments, you can, in fact, also write the data without the space separator:
```
curl -darguments http://example.com
```
---
## URL globbing
At times you want to get a range of URLs that are mostly the same, with only a small portion of it changing between the requests. Maybe it is a numeric range or maybe a set of names. curl offers "globbing" as a way to specify many URLs like that easily.
```
curl -O http://
```
### Numberic ranges
```
curl -O http://example.com/[1-100].png
```
also
```
curl -O http://example.com/[001-100].png
```
also with increment of 2
```
curl -O http://example.com/[0-100:2].png
```
### Alphabetical ranges
```
curl -O http://example.com/section[a-z].html
```
### A list
```
curl -O http://example.com/{one,two,three,alpha,beta}.html
```
### Combinations
```
curl -O http://example.com/{Ben,Alice,Frank}-{100x100,1000x1000}.jpg
```
Or download all the images of a chess board, indexed by two coordinates ranged 0 to 7:
```
curl -O http://example.com/chess-[0-7]x[0-7].jpg
```
And you can, of course, mix ranges and series. Get a week's worth of logs for both the web server and the mail server:
```
curl -O http://example.com/{web,mail}-log[0-6].txt
```


---
## Example:
### API: Upload a image
```
curl -X "POST" "https://api.16securities.org:20443/cerberus/omnibus/documents.upload" \
     -H 'Content-Type: multipart/form-data; charset=utf-8; boundary=__X_PAW_BOUNDARY__' \
     -F "checksum=5e872d1bf3c252e7e94ae2b98973a2094a95e7f1" \
     -F "file="
```
### API:Create Dwolla Customer
```
curl -X "POST" "https://api.16securities.org:20443/cerberus/internal/banking/dwollaCustomers.create" \
     -H 'Content-Type: application/json; charset=utf-8' \
     -d $'{
  "account_id": "XCTD-00010670"
}'
```
### API: get order info by stream（without header info，the common-line will be unauthorized）
```
curl -v "https://bss.16securities.org/ssi_api/flash/internal/api/normalOrder/stream?account_id=XCTR-00010026&client_id=XCTR&timeout=3" 2>/dev/null
```
`2>/dev/null`\
make the response simple exclude curl execute info

### API: get order info by stream
```
curl -v 'https://bss.16securities.org/ssi_api/flash/internal/api/normalOrder/stream?account_id=XCTR-00010026&client_id=XCTR&timeout=0' -H 'authority: bss.16securities.org' -H 'pragma: no-cache' -H 'cache-control: no-cache' -H 'accept: text/event-stream' -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36' -H 'sec-fetch-site: same-origin' -H 'sec-fetch-mode: cors' -H 'referer: https://bss.16securities.org/order/queue?page=1' -H 'accept-encoding: gzip, deflate, br' -H 'accept-language: en-US,en;q=0.9' -H 'cookie: lap2_sessionid=t3nyl9qr60ii97bkw7cl00u65jpikdz8' --compressed
```
* -H 'authority: bss.16securities.org'     传递author认证信息  
* -H 'pragma: no-cache'  
* -H 'cache-control: no-cache'  
* -H 'accept: text/event-stream'  表明这个请求建立是一个长连接，只要有新的数据更新就会被吐出来，而不要类似调用API接口，请求完就中断连接
* -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.108 Safari/537.36'    浏览器信息  
* -H 'sec-fetch-site: same-origin'  
* -H 'sec-fetch-mode: cors'  
* -H 'referer: https://bss.16securities.org/order/queue?page=1'   
* -H 'accept-encoding: gzip, deflate, br'   
* -H 'accept-language: en-US,en;q=0.9'  
* -H 'cookie: lap2_sessionid=t3nyl9qr60ii97bkw7cl00u65jpikdz8'  