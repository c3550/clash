# clash项目说明
>这个项目适用于`Koolshare梅林改版380/384/386固件`。 


项目两个分支：
- main分支： 支持380固件
- ksmerlin386分支： 支持384/386固件


## 使用满足条件

- CPU架构: Armv7l/Armv8 (能运行clash可执行程序)
- 路由器固件： Koolshare的官改、梅林改版的380/384/386固件
- 

## v1开头版本为支持KS梅林380版本固件

- [x] Clash服务启动开关
- [x] 透明代理启用开关: 选择是否需要使用透明代理(感觉不到自己使用了代理，内网应用不做任何配置即可访问Google)
- [ ] ~~网络状态检查(似乎这个功能有点多余)~~
- [x] 节点配置:支持provider(url)更新配置。
- [x] DNS设置：使用无污染的DNS解析国外域名。
- [x] 支持添加和删除个人代理节点(单独分组：命名为DIY)。
- [x] 更改URL订阅源方式为下载文件更新方式，更合理安全，避免URL无法访问导致Clash无法启动情况。

> 为了支持 ss/ssr/vmess URI后台解析，新增加了一个`uri_decoder`工具，目的是解析URI并生成新增加节点的yaml文件，最后使用`yq`命令合并两个文件，完成节点添加功能。


## v2开头版本为支持KS梅林384/386版本固件

与v1系列版本差别就是对`Koolshare`软件中心API的`1.5`版本支持。

由于差异比较大的缘故，单独分了一个分支进行维护。

目前支持功能：
- [x] 透明代理模式
- [x] URL订阅源更新(走路由器代理访问)
- [x] 支持DIY代理节点添加/删除功能(由于URI的不规范原因,支持的代理参数可能存在解析问题)
- [x] 代理组类型切换功能: select/url-test/load-blance/fallback

目前没做的功能：
- [ ] 皮肤定制，不打算搞
- [ ] 支持更复杂的URI解析配置，不打算搞，能用就行，不能用的时候再更新。
- [ ] 其他没想到的哈，如果你有更有用的功能或者需求，可以讨论交流。

## 为什么不提供代理可用性检测
> 因为检测代理可用性总要访问一些没必要的地址。即使检测了，有时候也是不能证明代理是否可用的！这就是多此一举的功能。

到底代理可不可用，验证就很简单，直接使用就可以了：
- **国外验证**直接通过浏览国外Youtube就可以验证了
- **国内验证** 访问国内网站就可以了。

## 订阅规则手动更新
> 增加手动更新 `ruleset`/`Country.mmdb`文件。

- 更新 `ruleset` ： 规则集下载。
- 更新 `Country.mmdb` ： 官方文件下载。

## 怎么使用？

```bash
git clone https://github.com/learnhard-cn/clash.git
rm -tr clash/.git
tar zcvf clash.tar.gz clash
```

或者， 到`Release`页面下载安装包 [https://github.com/learnhard-cn/clash/releases/latest](https://github.com/learnhard-cn/clash/releases/latest)

选择最新版本下载到本地，重命名为： `clash.tar.gz` 。

接下来就可以将这个安装包通过SSH传输到路由器上的`/tmp/`目录上，执行如下命令进行手动安装：

```bash
cd /tmp
tar zxvf clash.tar.gz
sh clash/install.sh
```
安装成功后，即可在`软件中心`里看到`clash`插件了。



## 为什么有这个项目

由于种种原因，某些路由器的固件停留在了`梅林380改版`，但是现在很多插件开发都不再支持`梅林380改版`了，例如`Clash`没有找到一个支持版本。

因此，就产生了这个项目。

## 主界面

![](./images/demo.png)

