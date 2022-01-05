# 规范与约定

> An unexamined life is not worth living —— Socrates

## Gitbook的使用

需详细了解请戳[指南](http://www.vapicloud.com/books/gitbook/), 常用操作如下:

```code

安装gitbook
# npm install gitbook-cli -g

在SUMMARY.md中编辑目录,并通过下面命令生成对应的文件和文件夹
# gitbook init

生成静态文件
# gitbook build

启动本地服务
# gitbook serve

```

## 约定

### 图片大小规范

不建议使用大文件,页面上满足基本的清晰度即可.大文件考虑放使用图床.

### 资源存储路径

文章需引入图片或其他资源时,需要存储在文章平级目录的asserts目录下.

Typora的设置建议参考下图:

![image-20210827155319945](asserts/image-20210827155319945.png)

