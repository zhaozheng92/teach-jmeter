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


