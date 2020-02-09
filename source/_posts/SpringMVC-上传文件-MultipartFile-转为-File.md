---
title: SpringMVC 上传文件 MultipartFile 转为 File
date: 2020-02-09 22:18:20
img: https://cdn.jsdelivr.net/gh/liangpengjie/mumuimgs/20200209223145.png
top: false
cover: false
coverImg: 
comment: false
tags:
  - SpringMVC
summary: 
password:
categories: Java
---


在使用 SpringMVC 上传文件时，接收到的文件格式为 `MultipartFile`，但是在很多场景下使用都需要`File`格式的文件，记录下以便日后使用。

> 以下`mFile`为`MultipartFile`文件
> 此方法会在本地产生临时文件，使用完毕需要删除
> 在网上搜索未发现可直接使用的不产生临时文件的方法，查到几个本地测试皆无法通过，如哪位有不产生临时文件的方法，请多多指教👍

## MultipartFile 转为 File
```java
File file = new File(mFile.getOriginalFilename());
FileUtils.copyInputStreamToFile(mFile.getInputStream(), file);
// 会在本地产生临时文件，用完后需要删除
if (file.exists()) {
    file.delete();
}
```

## MultipartFile 获取 Base64 编码
```java
File file = new File(mFile.getOriginalFilename());
FileUtils.copyInputStreamToFile(mFile.getInputStream(), file);
try (FileInputStream fis = new FileInputStream(file)) {
    byte[] buf = new byte[(int) file.length()];
    fis.read(buf);
    return new String(Base64.encodeBase64(buf), StandardCharsets.ISO_8859_1);
} catch (IOException e) {
    log.error(e.getMessage(), e);
} finally {
    if (file.exists()) {
        file.delete();
    }
}
```
