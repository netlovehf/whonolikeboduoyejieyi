# 利用宝塔面板实现阿里云DDNS更新

![1](https://user-images.githubusercontent.com/73426989/122664468-250fda80-d1d4-11eb-9b46-e882e16f0c2e.jpg)
编辑替换好下方脚本需要你填写的一些参数后，就可以照着上图直接进去保存即可。        
本脚本为单次运行后自动结束程序，所以适合使用宝塔的定时自动执行任务。       
其中的更新时间建议每天执行，当然也可以更频繁些，例如N小时一次。

参数说明：

AccessKey ID：          
aliddnsipv6_ak="**********"          

Access Key Secret         
aliddnsipv6_sk="************************"              

子域名：           
aliddnsipv6_name1='www'           

域名：          
aliddnsipv6_domain='xxx.com'          

TTL:          
aliddnsipv6_ttl="600"              

show:enp1s0 是指定网卡获取IPv6，可通过ifconfig命令来获取网卡名(如果报错enp1s0未找到，请自行获取网卡名替换上方脚本中的enp1s0为你获取到的正在连接的网卡名)              
ipv6s=`ip addr show enp1s0 | grep "inet6.*global" | awk '{print $2}' | awk -F"/" '{print $1}'` || die "$ipv6"       

配置好了之后保存，可以尝试执行一次看是否已经生效，如果正常就OK啦！是不是很简单？     

```
aliddnsipv6_ak="**********"
aliddnsipv6_sk="************************"
aliddnsipv6_name1='www'
aliddnsipv6_domain='xxx.com'
aliddnsipv6_ttl="600"

if [ "$aliddnsipv6_name1" = "@" ]
then
  aliddnsipv6_name=$aliddnsipv6_domain
else
  aliddnsipv6_name=$aliddnsipv6_name1.$aliddnsipv6_domain
fi

now=`date`

die () {
    echo $1
}

ipv6s=`ip addr show eth0 | grep "inet6.*global" | awk '{print $2}' | awk -F"/" '{print $1}'` || die "$ipv6"

for ipv6 in $ipv6s
do
  #ipv6 = $ipv6
  break
done

echo $ipv6

current_ipv6=`nslookup -query=AAAA $aliddnsipv6_name 2>&1`
#echo $current_ipv6

current_ipv6=`echo "$current_ipv6" | grep 'Address: ' | tail -n1 | awk '{print $NF}'`
echo $current_ipv6

if [ "$?" -eq "0" ]
then
    current_ipv6=`echo "$current_ipv6" | grep 'Address: ' | tail -n1 | awk '{print $NF}'`
    echo $current_ipv6

    if [ "$ipv6" = "$current_ipv6" ]
    then
        echo "skipping"
    fi
# fix when A record removed by manual dns is always update error
else
    unset aliddnsipv6_record_id
fi


timestamp=`date -u "+%Y-%m-%dT%H%%3A%M%%3A%SZ"`


urlencode() {
    # urlencode <string>
    out=""
    while read -n1 c
    do
        case $c in
            [a-zA-Z0-9._-]) out="$out$c" ;;
            *) out="$out`printf '%%%02X' "'$c"`" ;;
        esac
    done
    echo -n $out
}

enc() {
    echo -n "$1" | urlencode
}

send_request() {
    local args="AccessKeyId=$aliddnsipv6_ak&Action=$1&Format=json&$2&Version=2015-01-09"
    local hash=$(echo -n "GET&%2F&$(enc "$args")" | openssl dgst -sha1 -hmac "$aliddnsipv6_sk&" -binary | openssl base64)
    curl -s "http://alidns.aliyuncs.com/?$args&Signature=$(enc "$hash")"
}

get_recordid() {
    grep -Eo '"RecordId":"[0-9]+"' | cut -d':' -f2 | tr -d '"'
}

query_recordid() {
    send_request "DescribeSubDomainRecords" "SignatureMethod=HMAC-SHA1&SignatureNonce=$timestamp&SignatureVersion=1.0&SubDomain=$aliddnsipv6_name&Timestamp=$timestamp&Type=AAAA"
}

update_record() {
    send_request "UpdateDomainRecord" "RR=$aliddnsipv6_name1&RecordId=$1&SignatureMethod=HMAC-SHA1&SignatureNonce=$timestamp&SignatureVersion=1.0&TTL=$aliddnsipv6_ttl&Timestamp=$timestamp&Type=AAAA&Value=$(enc $ipv6)"
}

add_record() {
    send_request "AddDomainRecord&DomainName=$aliddnsipv6_domain" "RR=$aliddnsipv6_name1&SignatureMethod=HMAC-SHA1&SignatureNonce=$timestamp&SignatureVersion=1.0&TTL=$aliddnsipv6_ttl&Timestamp=$timestamp&Type=AAAA&Value=$(enc $ipv6)"
}

#add support */%2A and @/%40 record


if [ "$aliddnsipv6_record_id" = "" ]
then
    aliddnsipv6_record_id=`query_recordid | get_recordid`
    #echo '-----------------' $aliddnsipv6_record_id
fi
if [ "$aliddnsipv6_record_id" = "" ]
then
    aliddnsipv6_record_id=`add_record | get_recordid`
    echo "added record $aliddnsipv6_record_id"
else
    update_record $aliddnsipv6_record_id
    echo "updated record $aliddnsipv6_record_id"
fi
```
[参考原文链接](https://www.xiaobaike.net/thread-468.htm)
