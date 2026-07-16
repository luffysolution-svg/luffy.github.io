![PixPin_2026-06-28_22-00-34](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-28_22-00-34.png)**Fast Note Sync Plugin** 是一款Obsidian插件,在所有同步方案中最省钱，秒同步、笔记可转公网链接查看、还能作为Codex插件嵌入笔记

我相信不少Obsidian党们,还没有听说过他。

目前Obsidian同步常见方案有几类

但是都有各自的痛点：

- Obsidian Sync：省心，但需要持续订阅。
- 坚果云、WebDAV、网盘同步：便宜，但容易遇到冲突、附件和配置同步问题。
- Git 同步：适合技术用户，普通用户门槛偏高。
- 自建同步服务：一次配置，长期使用成本低。

Obsidian官方的同步功能费昂贵这没话说

![file-2026-06-28-21-53-27-755](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-755.png)

remotely save插件+OneDrive的方案虽然好用,但是也需要订阅服务,也要花不少钱

icloud同步的配置方案最简单,但是也是需要每个月收费

坚果云可以配合remotely save插件或者自己的Obsidian插件使用

但是免费方案空间少的可怜emmm

![file-2026-06-28-21-53-27-753](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-753.png)

恰好!

我今天刷b站看到Obsidian同步教程视频的底部评论区有这么一个新颖方案

**Fast Note Sync Plugin**

我翻了翻Obsidian插件市场,发现还真有!

![file-2026-06-28-21-53-27-769](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-769.png)

这是一个给Obsidian 做私有同步的服务端项目。服务端用Go + WebSocket，Web管理界面用React；需要配合Obsidian第三方插件Fast Note Sync PLugin使用。

项目地址：

[https://github.com/haierkeys/fast-note-sync-service](https://github.com/haierkeys/fast-note-sync-service)

他的核心功能是：

1. 多端同步 Obsidian笔记，支持Vault 自动创建、笔记 CRUD、秒级在线设备变更分发。

2. 可同步附件，比如图片、PDF等非 Markdown文件，并支持大文件分块上传/下载。

3. Web管理后台：创建用户生成插件配置、管理Vault和笔记内容。

4. 可以让脚本、自动化工具、AI手读写笔记文档

5. 可以通过MCP把你的笔记库接到 Cursor、Claude Code、Cherry Studio 等 AI客户端，让AI通过服务端读写笔记。

6. 还有历史版本管理、回收站、分享、短链、备份、Git 自动提交、多存储后端等功能

### 部署方式

目前支持Docker部署和脚本一键部署

```
bash <(curl -fsSL https://raw.githubusercontent.com/haierkeys/fast-note-sync-service/master/scripts/quest_install.sh)
```

### 同步实现方式

![file-2026-06-28-21-53-27-823](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-823.png)

### 注意事项

![file-2026-06-28-21-53-27-821](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-821.png)

### 具体部署实操

由于我用的是Windows11系统，然后我是个人使用，我第一次接触，我也不会，于是让Codex帮我部署

然后他告诉我：

正常自用：建议要域名 + HTTPS 证书

![file-2026-06-28-21-53-27-818](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-818.png)

如果不想买/备案域名：可以用 Cloudflare Tunnel/内网穿透

![file-2026-06-28-21-53-27-815](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-815.png)

然后我问他还需要注意什么？他说需要及时保存相关配置信息：

![file-2026-06-28-21-53-27-811](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-811.png)

哎，刚好我有cloudflare账号，那就浅浅试试吧

然后剩下的涉及到我的知识盲区，内网穿透，网关这些我不到哇

所以还是让Codex老爹帮我解决

注意这里给他开启所有权限，才可以进行

![file-2026-06-28-21-53-27-808](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-808.png)

然后大概过了7、8分钟他完成了

![file-2026-06-28-21-53-27-807](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-807.png)

紧接着根据Codex的步骤操作，我在浏览器访问那个地址

![file-2026-06-28-21-53-27-803](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-803.png)

到这一步进行配置

![file-2026-06-28-21-53-27-801](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-801.png)

之后就是生成授权命令后点击一键跳转到Obsidian进行配置

![file-2026-06-28-21-53-27-798](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-798.png)

不过最好还是复制保存这些配置信息防止忘记了

然后这里同步是真的话，2s内同步完我所有的文件，这要是坚果云，不得要花个10来分钟

![file-2026-06-28-21-53-27-794](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-794.png)



他的页面审美是真好看，操作也非常的丝滑

![file-2026-06-28-21-53-27-784](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-784.gif)

然后这个插件更新很活跃，在电报上可以向大佬求助

![file-2026-06-28-21-53-27-787](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-787.png)

最后这一步弄完之后

剩下的步骤就是到cloudflare里面完成

首先打开：

[https://one.dash.cloudflare.com/](https://one.dash.cloudflare.com)

然后进入：

Networks / Networking → Tunnels

登录Cloudflare dashboard->Networking >Tunnels，创建 tunnel。

![file-2026-06-28-21-53-27-777](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-777.png)

官方文档指南：

[[https:/developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/get-started/create-remote-tunnel/](https://github.com/developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/get-started/create-remote-tunnel/)](https:/developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/get-started/create-remote-tunnel/)

接着点击：`Create a tunnel`，然后选择：`Cloudflared`，名字建议填：`fast-note-sync`，然后到Connector安装页面时，选择Windows，Cloudflare会给你一条类似命令：`cloudflared.exe service install eyJhIjoi...`你只需要复制后面那段很长的：`eyJhIjoi...` 即可，这就是Tunnel token。

>remote-managed tunel 只需要token 就能运行，因此这个token要当密码保管。

然后把这个token发给Codex让他帮你进行配置

![file-2026-06-28-21-53-27-775](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-775.png)

参考文档：

[https://developers.cloudflare.com/tunnel/advanced/tunnel-tokens/](https://developers.cloudflare.com/tunnel/advanced/tunnel-tokens/)

最后是添加 Public Hostname:Subdomain: 

1. noteDomain：你的域名.
2. comType: HTTP
3. URL: localhost:9000

最终外部地址会是：

[https://note.你的域名.com](https://note.xn--6qqv7i2xdt95b.com/)

拿到这两个东西后发给AI让他帮你进行配置即可：

1. Tunnel token: eyJhIjoi..
2. 公网地址：https：//note.你的域名.com

它会帮你自动改：

`C:\Users\Administrator\Documents\fast-note-sync-service\config\config.yaml`

改这些项：server:

1. ext-api-url："[https://note.你的域名.com"security](https://note.xn--6qqv7i2xdt95b.com"security/):
2. webgui-login-token-bind-ip: false
3. cloudflare:enabled: true
4. token："你的tunneltoken"然后重启并验证公网访问。

顺带一提,需要自备域名

买完域名后，需要把 DNS 服务器改成 Cloudflare 给你的 nameserver。

![file-2026-06-28-21-53-27-752](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-752.png)

![file-2026-06-28-21-53-27-750](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-750.png)

另外,Cloudflare Zero Trust Free需要绑卡的,你可以跟Codex说一下,他会帮你改配置文件,不走这个路径

![file-2026-06-28-21-53-27-758](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-758.png)

这里我迂回了好久,帮大家踩个坑

![file-2026-06-28-21-53-27-756](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-756.png)

你就告诉Codex下面这段话:

- 不在 Zero Trust 里配置 Public Hostname。
- 在本机 `cloudflared` 启动时加 `--url http://localhost:9000`。
- 在 Cloudflare 普通 DNS Records 里手动添加 CNAME 到 `TunnelUUID.cfargotunnel.com`。

这一步完成之后剩下的就是注册,然后登录,再回来让Codex关闭注册系统

![file-2026-06-28-21-53-27-773](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-773.png)

搞定之后就大功告成了哈哈哈!

![file-2026-06-28-21-53-27-770](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-770.png)

爽哉爽哉!

不过这里我购买了腾讯云比较便宜的域名来使用

一年14元,续费33每年,不过至少比坚果云和one drive  iCloud等平台便宜很多了

而且同步效果简直夯爆了!

![file-2026-06-28-21-53-27-791](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-791.gif)

不过我听说还有更便宜的方案,好像是直接cloudfire购买域名还更方便,续费也便宜

不过碍于我没有国际visa或者招商visa黑金卡等等支付渠道

暂时不管那么多了,能用就行

桌面端效果如下:

![file-2026-06-28-21-53-27-745](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-745.png)

手机端效果如下:

![file-2026-06-28-21-53-27-748](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-748.jpg)

同步只用了1s左右hhh

而且啊,笔记还能导出分享,又解决了Obsidian官网付费才有的功能


![file-2026-06-28-21-53-27-743](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/file-2026-06-28-21-53-27-743.gif)

**Fast Note Sync Plugin**

我真要给你个夯中夯的评分,简直夯爆了,说这是目前最好用的同步方案也不为过

那么,以上就是本期的Obsidian同步方案教程

既然都看到这里了,如果觉得对你有所帮助,不妨随手点个赞、转发支持一下吧，如果想要第一时间收到推送，也可以给我个星标🌟~ 谢谢你看我的文章，我们，下次再见。