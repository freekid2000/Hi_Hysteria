## 常见问题/通知

### 下面给出的常见问题无法解决你的疑问?

应要求创建了一个TG群，帮助大家交流使用hysteria2过程中遇到的问题

[https://hihysteria.t.me/](https://hihysteria.t.me/)

### 重要通知留档#占位

这里可能有你解决问题的提示，有些时候hysteria的配置新版本和旧版本无法兼容导致出错

**很多时候出问题了更新服务端和客户端配置都能解决**

### 常见问题

这里整理了一些常见的关于hihy使用过程中的问题，你如果遇到请不要急着开issue请在这里找一下说不定能解决。~~不要再开一些没有意义的issue了~~

#### 1.hysteria2速度一直提不上去怎么办?

这个问题很笼统，你需要知道客户端和服务端都有瓶颈，如果需要极高的网络带宽服务端和客户端都要有相应的硬件支持和带宽支持。

QUIC比原生TCP对硬件的开销要大很多，往往很多时候限制你的是你的CPU

如果你使用的是udp协议，这时就需要保证你本地的ISP没有对udp传输做限制，而且少部分IDC提供者也会对udp做限制，防止用户拿来滥用

不要随便填写上行带宽和下行带宽，按照自己真实水平填写，大于你cpu处理能力和网络带宽能力的期望也会有这个问题

最后对于某些用这种lxc/openvz虚拟化无法更改 `net.core.rmem_max`，会导致在填写过高带宽时无法很好支持

#### 2.一直无法连接怎么办？连接报错怎么办？有时可以用，有时不能用怎么办？

首先你要保证你的服务端能正常启动

其次能保证你客户端配置没有报错

如果日志还表现为 `[error:timeout: no recent network activity] Failed to initialize client`

请查看你的IDC是否在[黑名单](blacklist.md)里,如果以上都不满足请看下方

* 你没有打开云平台的防火墙，很多时候本机防火墙和云防火墙是分开的，hihy会自动打开本地防火墙，云防火墙需要你手动启动，关于启动说明看[这里](firewall.md)
* 你本地使用的ISP限制严格无法通行非常规udp协议，请切换协议类型尝试或者用faketcp
* 配置错误没有察觉，请重新检查一遍
* 你的IDC未被黑名单收集，请到此[issue](https://github.com/emptysuns/Hi_Hysteria/issues/9)提交

#### 3.提示不支持此系统怎么办？

你的系统太老了，不是主流社区维护的版本，比如软件更新源已经不支持更新了，这种系统单靠脚本是很难支持全的，这里就自己解决了

或者你的系统经过了服务提供商魔改，hihy无法识别系统类型这就无法进行接下来的步骤，也会报错

这种问题请自己安装成当前主流的镜像，方法很多这里就不说明了

#### 4.脚本无法正常启动

每次运行 `hihy`都需要通过github获取最新信息，你的ip可能被github拉黑了或者根本无法连接github

#### 5.用hysteria2会被墙吗？

目前未被针对，不知道以后如何，就算被针对由于是开源项目也会有很多人贡献代码对抗封锁的，参考隔壁ss。在这里感谢hysteria2的开发者做的无私贡献。

#### 6.Sagernet / Matsuri/Nekobox无法连接问题

请在github或者google play商店装上Hysteria-plugin并且**允许被其他应用启动**
现在不推荐使用sagernet,已经停止更新好长时间了,建议使用nekobox

#### 7.cpu占用这么高，hihy不会藏挖矿了吧？

:)

所有渣代码没有加密，短链接使用的git.io，无法根据client不同返回不同值

即**均可查，童叟无欺**

占用高是QUIC的特点

#### 8.如何选择是否使用obfs混淆

obfs是用来混淆流量成未知流量的选项，开启它将会最大程度的对抗封锁，但是有优点和缺点
优点：

1. 抗封锁
2. 未知流量安全性强
3. 能够隐藏证书握手信息，可以配合使用自签证书

缺点：

1. 对cpu开销大，如果性能不好会影响速度
2. 对某些有协议白名单的IDC来说，未知udp流量往往被认为是攻击，遭到阻断，客户端无法连接到服务端

#### 9.关于自签证书的解疑

目前自签证书使用的CA是固定的，是Tencent Root CA，这肯定是不合法的，请不要使用敏感域名，比如wechat.com


#### 10、PC端没问题，移动端nekobox和v2rayn无法访问cloudflare等等网站，提示http/3错误

打开 **路由 -> 屏蔽QUIC**功能即可
nekobox/v2rayNForAndriod在路由里面打开屏蔽QUIC功能，否则无法访问使用了http/3的网站。
此问题由于服务器屏蔽了udp/443流量，hysteria对udp无增强的拥塞控制效果，所以在服务端上这个功能是必须的


### 10. 待补充...
