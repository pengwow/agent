
# agent
## 概述

## 开源计划
* 时间：2020-4

## 功能特性
### 文件分发与传输
#### 传输模式：
BT模式——对于大小大于10KB的文件，将自动启用BT作为首选传输方式；
直传模式——对于10KB以下的文件，将使用tcp直传模式；
混合模式——在BT模式下，如果发生BT传输持续性失败，则会尝试使用直传模式传输BT文件分片；当BT传输恢复时，则停止直传模式；
#### 传输类型：
文件传输——分发单个文件到指定机器，这里文件可以是任何格式，任何可读目录下的可读文件；文件分发完成后，会自动同步目标文件权限与源文件一致；对于直传模式，文件传输结束后会进行MD5校验，对于BT模式和混合模式，会进行hash值校验文件的完整性；
#### 传输控制：
区域链控制——让文件沿着指定的路径，通过多个中转节点的接力，最终到达目标机器，并且源文件和目标文件所在机器不在同一个物理或逻辑区域。我们称这种传输方式为区域链传输。区域链控制是指通过一定规则指定文件中转的路径，以满足具有特殊专线链接的两个区域间的传输需求。
跨区域穿透——跨区域穿透是指原本相互隔离的两个区域，但是由于特殊目的，需要就本次传输进行定向穿透。适当修改配置来完成这种定向穿透。
### 实时任务执行
#### 任务类型：
命令类型——linux支持bash命令、windows支持cmd命令、AIX支持ksh命令，支持各种自定义可执行文件格式程序的启动，支持各种解释性语言程序的执行。
脚本类型——linux支持shell脚本、windows支持bat脚本（安装有cygwin的额外支持shell脚本）、powershell、AIX支持ksh脚本，以及各种系统支持的解释性脚本程序。
#### 任务控制：
指定用户——linux及其他类linux系统支持按指定用户执行任务，例如用户设定以user00用户执行ps，则只能看到该用户权限范围内的结果；因为windows操作系统的限制，只有开启校验机器密码（见下文）功能的用户才能指定用户执行任务，否则都以administrator用户执行任务。
继承用户环境——linux及其他类linux系统支持指定用户后继承该用户设定的环境变量；Windows无此功能。
校验机器密码——企业版用户可以选择是否校验机器密码，如果选择不校验，则window Agent不支持按指定用户执行任务的功能。
有害操作告警——管控系统能够对高危操作进行预警，高危操作的定义由系统自动设定。
有害操作防护——管控系统能够对高危操作进行预警并干预，高危操作的定义及干预措施提供选项供用户配置。
### 数据采集与传输
#### 数据采集服务：
自定义数据采集——Agent开放数据发送接口、cmdline及SDK，供用户开发自定义的数据采集程序或脚本。
采集器插件化支持——Agent支持采集器插件化，自动加载采集插件，并监控插件的存活状况。如果采集插件异常终止，则重新拉起采集插件；如果多次拉起失败则告警。
实时数据快照——管控平台支持缓存安装有Agent的机器1min内的快照数据，并提供接口供用户访问。
动态负载均衡——由于Agent数据采集的量大，且具有随业务特性波动的特点，这些数据在流转时需要高性能的服务端做收敛转发，为了提高服务端机器的利用率，减少由于数据量变化时带来的负载不均衡问题，管控系统支持按分钟级别动态调整数据转发的通道，以达到集群内服务端负载均衡的目的。
### 集群管理
自动服务发现：管控平台同一个集群内的模块均支持自动发现，用户扩缩容任何节点，系统均能实时感知，并调整通讯策略，保证服务的高可用。
集群负载均衡：管控平台同一个集群内，支持按照Agent链接数进行负载均衡。
Agent状态查询：管控平台提供接口，查询Agent状态。接口按照实时性分为两类：一类为实时状态接口，只能查询当前Agent是否正常；二类接口提供24s内的状态查询，查询的内容包括Agent上次心跳时间、Agent版本、Agent使用的cpu、Agent使用的mem。
多区域负载均衡：管控平台支持对同一集群进行不同区域的划分，不同区域按照各区域内的负载均衡规则处理；未划分区域的Agent按照集群负载均衡策略处理。

## 支持OS
* 未来目标支持全部操作系统
CentOS
Redhat
Debian
SUSE
Ubuntu
Windows Server
AIX


参考：https://docs.bk.tencent.com/gse/