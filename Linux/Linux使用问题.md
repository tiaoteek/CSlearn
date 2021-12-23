### 查找Linux上某个软件的相关包

```bash
dpkg --get-selections  |grep libreoffice
```

### 软件删除问题

apt-get remove 与 apt-get purge功能相近，remove删除不清除配置文件，purge会删除

