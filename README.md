# teach-jmeter
我是tony老师,以后这个仓库就专门用来教学 jmeter使用.
先说下,jmeter 其实是一个压测工具,**但是也可以用来做接口上的一键流程化测试**,
本来我不想搞这个,但是最近经理改了个类,然后发生了一些不可描述的事情,导致我要返工改字段,
改了字段还要自测. 问题就是: 设计的那个模块自测,有2种语言,5个类型,每个还有5个子类,事件情况有3种 这就导致了 我一次全面测试要 将近一百多次 每次耗时估计在3分钟左右.
就很绝望,所以想起来了jmeter. 大佬不是卷么,那我就彻底卷起来,教测试用神器,来测系统.卷起来了,然后我就跑.
## 备注
- 使用jmeter 要JDK8+的环境,所以自己再去下载一个jdk 链接: https://adoptopenjdk.net/
## 下载
- 网站: http://jmeter.apache.org/download_jmeter.cgi

## 教学
- PS: 这次我的jmeter安装路径是: **D:\Program Files\apache-jmeter-5.4.1\bin** , 默认jmeter的根目录是: **D:\Program Files\apache-jmeter-5.4.1**,所以后续操作 自己目录替换;
### 常规
- 先启动 在目录bin下有两个: `jmeter.bat` ,`jmeter.sh`
- win 双击bin下的**jmeter.bat**
- macOS 在命令行执行: ./bin/jmeter.sh 
- 启动后,可以看到出现了一个东西
![image](https://user-images.githubusercontent.com/33167955/124236258-d0138300-db48-11eb-9f2c-8ef88c0f17dc.png)
- 默认的是英文+黑色页面
- 先把语言和界面调成 中文和亮色调,黑色的看着很难受.
- 调颜色,如下图,设置好以后,会要求你重启,点Yes就行了.
![image](https://user-images.githubusercontent.com/33167955/124236463-0a7d2000-db49-11eb-8629-07b75a2b5425.png)
- 调语言
  - 第一种:在`/bin/jmeter.properties` 找一行 为 `#language=XX`的类似的 去掉 #号,然后=zh_CN 保存 重启jmeter 如下图
  - ![image](https://user-images.githubusercontent.com/33167955/124237013-ad359e80-db49-11eb-99d2-7ed255d17aa3.png)
  - 第二种如下图
  - ![image](https://user-images.githubusercontent.com/33167955/124236909-8c6d4900-db49-11eb-904b-d781ecf52400.png)

设置完.接下来我们开始搞一个简单的DEMO 测试HTTP




# 一些有用的备注:
## 请求https时,需要认证怎么办;
看链接: https://www.cnblogs.com/majestyking/p/12293195.html
修改: bin/jmeter.properties
查找 `server.rmi.ssl.disable=false` 把它的#号去掉,然后改为: server.rmi.ssl.disable=true
即忽略ssl认证.

## 提取Json数组的数据怎么办.
https://blog.csdn.net/qq_36502272/article/details/88529412

## 文件下载时,怎么弄呢

https://blog.csdn.net/qq_42947235/article/details/108882072

大致可以这么做:首先请求文件下载API,
接口返回成功,且ResponseHeaders 中有一个:

`Content-Disposition: attachment; filename=*`

这样的内容,那么我们可以使用正则提取器,把ResponseHeader里的文件名称提取出来.

正则提取器: 
```text
要检查相应字段: 信息头/ResponseHeader
引用名称: fileName
正则表达式: Content-Disposition: attachment; filename=(.+?)\n
模板: $1$
匹配数字: 0
```

然后借助beanShell Processor 进行文件保存.
```text
传递给BeanShell 参数:
参数: ${fileName}

script:

import java.io.*;
byte[] result = prev.getResponseData(); 
String name =new String(bsh.args[0].getBytes("ISO-8859-1"),"UTF-8");
#备注,由于我测试的项目中,最终拼接的filename是用ISO-8859-1 进行编码的,所以我这里进行了转码为UTF-8
#这样在保存的时候,文件名称不会乱码
String file_name = "C:\\Users\\Administrator\\Downloads\\jmeter\\"+name; 
File file = new File(file_name); 
FileOutputStream out = new FileOutputStream(file);
out.write(result);
out.close();



```




