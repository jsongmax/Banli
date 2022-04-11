# Banli-高危资产识别和高危漏洞扫描

Banli是一款极其简单好用的高危资产识别和高危漏洞扫描工具。本项目也是自己深入学习理解Go语言后计划陆续发布的项目之一。本项目仅用于安全研究人员在授权的情况下使用，请遵守网络安全法，若因本工具产生任何问题，后果请自负，与作者无关！程序代码中不会添加任何形式的后门，运行程序一般情况不会对系统产生危害，请各位师傅放心使用！本项目会持续更新，直到海枯石烂。作者：[0e0w](https://github.com/0e0w)。

本项目创建于2021年10月16日，最近一次更新时间为2022年4月12日。**每月15日定期更新！**

- [01-基本介绍](https://github.com/Goqi/Banli#01-%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D)
- [02-设计思路](https://github.com/Goqi/Banli#02-%E8%AE%BE%E8%AE%A1%E6%80%9D%E8%B7%AF)
- [03-使用说明](https://github.com/Goqi/Banli#03-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E)
- [04-更新记录](https://github.com/Goqi/Banli#04-%E6%9B%B4%E6%96%B0%E8%AE%B0%E5%BD%95)
- [05-未来计划](https://github.com/Goqi/Banli#05-%E6%9C%AA%E6%9D%A5%E8%AE%A1%E5%88%92)
- [06-致谢项目](https://github.com/Goqi/Banli#06-%E8%87%B4%E8%B0%A2%E9%A1%B9%E7%9B%AE)

## 01-基本介绍

我们养了一只比熊犬，她的名字叫板栗。她时而很活泼，时而又很安静，像极了这个Banli。

- **因为活泼**，所以她可以高效快速的进行高危资产识别和高危漏洞扫描。
- **因为安静**，所以她的动静很小尽可能的不被安全设备发现。

Banli可以对内外网的系统进行高危资产识别和高危漏洞扫描。方便渗透测试和红队评估人员进行快速识别高危资产，快速利用高危漏洞，从而最终拿到系统权限！

## 02-设计思路

Banli要解决的问题是如何快速识别企业的高危资产，如何快速扫描企业的高危漏洞。包括Web资产、中间件资产、框架资产、安全设备等高危资产的识别，包括Web漏洞、命令执行漏洞、反序列化等高危漏洞的扫描。项目设计时考虑到了尽可能的避免触发安全告警。设计思路包括多利用404页面，少用特定的后台等敏感页面等。具体的设计实现方式后续会公开！

2022年1月2日准备在本项目中集成其他的安全扫描工具！

## 03-使用说明

程序设计时遵循简单原则。项目尽可能的去掉了用户可控参数，因此所有参数用户都无法自定义。**1.资产识别功能都是对当前路径的urls.txt文件进行扫描，支持多种URL格式，一行一个，不能存在无效的URL格式！2.漏洞扫描模块都是对资产识别之后自动生成的文件进行扫描。** 例如：通过命令Banli.exe is seeyon扫描Seeyon资产，如果存在Seeyon资产，则自动创建isSeeyon.txt文件。之后可以使用Banli.exe hack seeyon对isSeeyon.txt文件内的资产进行Seeyon漏洞扫描。**减少无用功，拒绝无效努力！**

**一、资产识别**

- 说明：设计初衷是对单个高危资产进行扫描，一次性扫描多个资产效率较低。
- 支持识别的资产应用：activemq、ax2、baota、cas、confluence、coremail、dcuz、druid、dubbo、elasticsearch、exchange、eyoumail、finereport、flink、gerapy、gitlab、gogs、hadoop、harbor、hongfanoa、jboss、jeecms、jellyfin、jenkins、jinheroa、jira、jumpserver、jupyter、kibana、kingdee、kylin、landrayoa、leagsoft、liferay、metabase、mobileiron、nacos、ofbiz、phpmyadmin、rabbitmq、saltstack、seeyon、shiro、skywalking、solr、sonarqube、spark、springboot、struts、swagger、thinkphp、tomcat、tongdaoa、vesystem、vmware、wanhuoa、weaveroa、weblogic、websphere、yapi、yonyou、zabbix、zentao。
- 资产支持列表：Banli.exe is
- 所有资产扫描：Banli.exe is all
- OA 资产扫描：Banli.exe is oa
- 内网资产扫描：Banli.exe is nei
- 外网资产扫描：Banli.exe is wai
- 单个高危资产扫描：Banli.exe is log4j
  - 使用Banli.exe is log4j扫描那些组件资产用到了log4j。运行结束后存在的资产会保存到对应的文件中。
- ~~爆破高危端口扫描：Banli.exe is db~~

**二、漏洞扫描**
- 支持扫描的框架漏洞：seeyon、druid、weblogic、log4j、grafana、apisix、spring。
- 漏洞支持列表：Banli.exe hack log4j
  - jndiserver.txt中替换成自己的dnslog平台，扫描完成后在自己的dnslog上面看记录。
  - 使用Banli.exe hack log4j扫描log4j的资产是否存在漏洞，概念验证，无法获取权限。
  - 目前：支持Druid、Flink、JSPWiki、OFBiz、SkyWalking、Solr、Struts2、CAS、MonbileIro User Portal、Seeyon、Unifi Network、VMware HCX、VMware Horizon、VMware NSX、VMware vCenter、VMware vRealize、VMware Workspace One、Zipkin
- 单个漏洞全部资产扫描：Banli.exe hack seeyon

**三、信息收集**

- title获取：Banli.exe title

**四、资产发现**：待实现

**五、端口扫描**：数据库端口扫描已经实现！待公开

**六、密码爆破**：高危端口的账号密码爆破已经实现！待公开

## 04-更新记录

- 2022年4月15日：1.增加高危爆破端口扫描、增加密码爆破功能（功能已经实现，效果不佳，下个公开版公布）。2.新增Zipkin资产识别。3.新增18个Log4j2相关组件的漏洞扫描（Banli.exe hack log4j2）。4.程序大量优化，优化识别规则多线程等问题。
- 2022年4月8日：今天本程序被一些微信群推荐，感谢。优化程序，更新代码逻辑。
- 2022年2月15日：1.修复默认线程数太高导致内存指针报错的问题，添加用户可自定义线程数，感谢@T-T。
  2.支持单个资产的识别，感谢@ᗡD。v0.91版本暂时不对外公开！
- 2022年1月15日：添加随机UserAgent。添加日志记录。添加APISIX漏洞扫描模块。
- 2021年12月15日：新增37个资产识别。支持log4j、grafane、weblogic等部分漏洞扫描识别。完善优化程序，去除https证书过期导致无法识别的问题等。发布v0.8版本。
- 2021年11月15日：支持Seeyon漏洞扫描。添加新的资产识别。优化程序，发布v0.7版本。
- 2021年10月29日：添加支持新的资产识别，优化程序。发布v0.6版本。
- 2021年10月20日：添加单个资产的扫描方式。例：Banli.exe is thinkphp
- 2021年10月19日：支持Title扫描。支持内网资产和外网资产分开扫描。
- 2021年10月18日：添加新的资产识别，Chestnut更名为Banli。
- 2021年10月17日：优化程序，支持扫描单个资产列表，加入漏洞扫描功能。
- 2021年10月16日：项目框架基本完成。

## 05-未来计划

- 添加敏感路径爆破收集功能。添加资产发现模块。
- 添加资产端口扫描。添加其他类型资产识别：如数据库资产。
- urls.txt去重。内网存活资产发现。
- 资产识别或漏洞扫描之后将结果发送到指定邮箱。
- 添加账号密码爆破功能。

## 06-致谢项目

本项目开发过程中参加了这些项目的代码思路等！感谢这些作者，感谢开源社区！
- https://golang.org
- https://github.com/Goqi/Banli
- https://github.com/veo/vscan
- https://github.com/JKme/cube
- https://github.com/r0eXpeR/fingerprint
- https://github.com/0x727/FingerprintHub

## Stargazers

[![Stargazers @Goqi/Banli](https://reporoster.com/stars/Goqi/Banli)](https://github.com/Goqi/Banli/stargazers)

## Forkers

[![Forkers @Goqi/Banli](https://reporoster.com/forks/Goqi/Banli)](https://github.com/Goqi/Banli/network/members)

![](Banli/wx.png)

[![Stargazers over time](https://starchart.cc//Goqi/Banli.svg)](https://starchart.cc/Goqi/Banli)