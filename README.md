# TraceFinder使用手册

## 简要说明

	该项目为一款Windows维权排查工具，主要目的是为了减轻蓝队人员、应急响应以及安全工程师日常排查压力，达到快速分析的目的。执行完成后，能够快速检索常见后门，如果未排查出，请根据实际情况，使用常见应急响应工具做进一步安全排查。

## 鸣谢

感谢github开源社区各位大佬的项目，该项目参考以下golang项目：

[m-sec-org/d-eyes: D-Eyes为M-SEC社区一款检测与响应工具 (github.com)](https://github.com/m-sec-org/d-eyes)

[akkuman/EvilEye: A BeaconEye implement in Golang. It is used to detect the cobaltstrike beacon from memory and extract some configuration. (github.com)](https://github.com/akkuman/EvilEye)

## 使用方式

### Windows后门排查

	该功能涵盖应急响应中常见后门排查的位置，针对计划任务、自启动、组策略、映像劫持等进行排查，同时引入内存查杀，查杀C2进程。

	使用方式TraceFinder.exe -check

​![image](https://github.com/user-attachments/assets/02d2ea22-2be1-4821-8482-992f1f8bb6da)
![image](https://github.com/user-attachments/assets/8d0d3046-33a9-4e0f-abdd-de1b14b49125)

### 文件分割

	开发该该功能，主要是在应急响应过程中，部分服务器日志，未根据日期进行生成，可能就会导致我们看到的服务器日志非常大，可能10G甚至几十G的日志文件，导致我们不能直接使用常见文本编辑器进行查看，通过该功能，能够直接将文件切割成指定大小，方便后续进行日志分析工作。

	使用方式：TraceFinder.exe -file 指定文件 -size 切割大小 -split

	ps：split表示为切割指令

![image](https://github.com/user-attachments/assets/d56dd746-b42a-4ca9-b9ec-f79349ffb459)
​![image](https://github.com/user-attachments/assets/37d827fc-cb5e-4647-a6bd-04be1a47c61e)

### 字符串查找

	常见字符串查找方式我们可以通过文本编辑器进行查看，但是如果存在大文件的场景，可能导致我们不能使用，这里开发此功能，能够快速检索到我们想要的字符串信息，如在日志分析中，我们发现一台主机存在dnslog外连场景，但是仅存在EDR，无流量监测设备的场景下，查看大文件日志，能够快速判断是否存在get请求，或者是查找我们想要的关键字信息。

	这里以查询dnslog地址ceye.io为例，能够快速查找出dnslog在该文件存在的行数，以及该行数据相关信息

	使用方式：TraceFinder.exe -file 指定文件 -target 目标字符串 -view

	ps：-view执行，主要是在控制台显示
![image](https://github.com/user-attachments/assets/36308445-5faf-4d9d-957a-e82822b0eb3f)​

## 后续开发计划

	1、后续考虑引入yara，对文件以及内存展开扫描

	2、常见组件安全排查，如Fastjson、Log4j、Shiro、ApacheMQ等

	........

	各位观众老爷如果有什么好玩的想法都可以在issue提，后续根据实际情况展开开发
