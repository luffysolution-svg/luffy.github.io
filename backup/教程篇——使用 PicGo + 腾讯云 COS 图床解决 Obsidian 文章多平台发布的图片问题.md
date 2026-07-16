## 一、为什么需要图床？

我平时习惯在 Obsidian 里写文章，Obsidian 的本地写作体验很好，尤其适合用 Markdown 管理长文、笔记和素材。

但是，当我想把 Obsidian 里的文章发布到微信公众号、知乎、飞书、小红书等平台时，会遇到一个很常见的问题：

> Obsidian 里的图片大多是本地附件，直接复制文章到其他平台时，图片无法正常显示。

比如 Obsidian 里的图片可能是这样的：

```markdown
![[Pasted image 20260629111215.png]]
```

或者：

```markdown
![](attachments/PixPin_2026-06-29 11-12-15.png)
```

这些图片路径只在本地电脑有效。复制到微信公众号、网页编辑器、Markdown 排版工具后，平台无法访问我电脑里的本地图片，所以图片就会丢失。

因此，我需要一个方案：

```text
Obsidian 本地图片
        ↓
自动上传到图床
        ↓
替换成公网图片链接
        ↓
复制到各个平台都能正常显示
```

经过测试，我最终采用了：

```text
Obsidian + PicGo + 腾讯云 COS 图床
```

这个方案比较稳定，也适合长期使用。

---

## 二、整体方案思路

整体流程如下：

```text
在 Obsidian 中写文章
        ↓
插入或粘贴本地图片
        ↓
通过 PicGo 上传图片到腾讯云 COS
        ↓
Obsidian 中的本地图片链接替换为图床链接
        ↓
复制 Markdown 内容到公众号 / 知乎 / 飞书 / 排版工具
        ↓
图片可以正常显示
```

最终文章中的图片会变成类似这样的公网链接：

```markdown
![](https://your-bucket-125xxxxxxx.cos.ap-guangzhou.myqcloud.com/Obsidian/20260629111215.png)
```

这样图片不再依赖本地路径，而是变成了可以被其他平台访问的网络图片。

---

## 三、准备工作

需要准备以下内容：

```text
1. 腾讯云账号
2. 腾讯云 COS 对象存储
3. PicGo 或 PicList
4. Obsidian
5. Obsidian 图片上传插件
```

这里不需要购买云服务器，也不需要轻量应用服务器。

真正需要的是：

```text
腾讯云 COS 对象存储
```

COS 的作用就是存放图片，并提供公网访问链接。

---

## 四、购买腾讯云 COS

进入腾讯云控制台，搜索：

```text
对象存储 COS
```

对于个人图床，建议先使用按量计费，或者购买一个较小规格的标准存储容量包。

推荐配置：

```text
产品：对象存储 COS
存储类型：标准存储
资源包：标准存储容量包
规格：10GB 起步
地域：中国大陆通用，或者选择广州 / 上海 / 南京 / 北京等地域
```

个人文章配图、截图、公众号素材等，10GB 起步通常已经够用。

不建议一开始购买：

```text
云服务器
轻量应用服务器
CDN
多 AZ 存储
低频存储
归档存储
```

这些对于个人图床来说不是必需项。

---

## 五、创建 COS 存储桶

进入：

```text
腾讯云控制台 → 对象存储 COS → 存储桶列表 → 创建存储桶
```

![PixPin_2026-06-29_11-30-20.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-30-20.png)

建议配置如下：

```text
存储桶名称：自定义，例如 obsidian-image-bed
地域：ap-guangzhou / ap-shanghai / ap-nanjing 等
存储类型：标准存储
数据冗余策略：单 AZ 存储
访问权限：公有读私有写
```

![PixPin_2026-06-29_11-31-06.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-31-06.png)

其中最重要的是访问权限。

建议选择：

```text
公有读私有写
```

![PixPin_2026-06-29_11-33-35.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-33-35.png)

含义是：

```text
公有读：别人可以通过图片链接访问图片
私有写：只有我自己或者持有密钥的工具可以上传、修改、删除图片
```

不建议选择：

```text
私有读写
```

因为这样图片外链可能无法直接访问。

也不建议选择：

```text
公有读写
```

因为安全风险较高。

然后记得创建好文件夹并设置文件夹也是公可读不可写的权限

![PixPin_2026-06-29_11-34-43.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-34-43.png)

![PixPin_2026-06-29_11-36-19.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-36-19.png)

---

## 六、记录存储桶信息

创建完成后，需要记录几个关键信息。

假设我的存储桶是：

```text
obsidian-image-bed-1251234567
```

那么：

```text
Bucket：obsidian-image-bed-1251234567
APPID：1251234567
Region：ap-guangzhou
```

其中：

```text
Bucket = 完整存储桶名称
APPID = Bucket 后面的数字部分
Region = 存储桶所在地域
```

例如：

```text
Bucket：obsidian-image-bed-1251234567
APPID：1251234567
Region：ap-guangzhou
```

注意：Bucket 一般要填写完整名称，也就是带 APPID 后缀的名称。

---

## 七、获取 SecretId 和 SecretKey

PicGo 上传图片到腾讯云 COS，需要使用腾讯云的 API 密钥。

进入：

```text
腾讯云控制台 → 访问管理 CAM → 访问密钥 → API 密钥管理
```

创建或查看密钥，获取：

```text
SecretId
SecretKey
```

注意事项：

```text
1. SecretKey 通常只在创建时完整显示，需要及时保存
2. 不要把 SecretId 和 SecretKey 发给别人
3. 不要把密钥截图发布到网上
4. 长期使用建议创建子用户，并只授权 COS 相关权限
```

如果密钥已经泄露，建议立即删除旧密钥，重新生成一组。

---

## 八、配置 PicGo 腾讯云 COS

打开 PicGo，进入图床设置，选择：

```text
腾讯云 COS
```

然后填写：

```text
SecretId：腾讯云 API 密钥中的 SecretId
SecretKey：腾讯云 API 密钥中的 SecretKey
AppId：你的 APPID
Bucket：完整存储桶名称
Region：存储桶地域
存储路径：Obsidian/
自定义域名：先留空
```

![PixPin_2026-06-29_11-31-49.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-31-49.png)

示例：

```text
SecretId：AKIDxxxxxxxxxxxxxxxx
SecretKey：xxxxxxxxxxxxxxxx
AppId：1251234567
Bucket：obsidian-image-bed-1251234567
Region：ap-guangzhou
存储路径：Obsidian/
自定义域名：留空
```

重点检查：

```text
Bucket 必须是完整 Bucket，例如 obsidian-image-bed-1251234567
Region 必须和存储桶实际地域一致
存储路径建议写 Obsidian/，不要写 /Obsidian/
自定义域名先不要填
```

配置完成后，可以在 PicGo 里上传一张图片测试。

如果上传成功，会生成类似这样的链接：

```text
https://obsidian-image-bed-1251234567.cos.ap-guangzhou.myqcloud.com/Obsidian/example.png
```

把链接复制到浏览器打开，如果能正常显示，说明腾讯云 COS 图床已经配置成功。

---

## 九、处理图片无法显示的问题

如果上传成功，但图片链接无法显示，可以按下面顺序排查。

### 1. 检查访问权限

进入：

```text
腾讯云 COS → 存储桶 → 权限管理
```

确认访问权限是：

```text
公有读私有写
```

如果是私有读写，外链图片可能无法打开。

---

### 2. 检查 Bucket 和 Region

PicGo 里的 Bucket 必须填写完整名称：

```text
obsidian-image-bed-1251234567
```

不要只填：

```text
obsidian-image-bed
```

Region 也必须和存储桶一致。

例如存储桶在广州，就填写：

```text
ap-guangzhou
```

---

### 3. 避免文件名带空格

图片文件名如果带空格，部分 Markdown 编辑器或平台可能解析失败。

不建议：

```text
PixPin_2026-06-29 11-12-15.png
```

建议：

```text
PixPin_2026-06-29_11-12-15.png
```

或者直接使用时间戳命名：

```text
20260629111215.png
```

如果链接里已经有空格，可以把空格替换成：

```text
%20
```

例如：

```markdown
![](https://your-bucket.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29%2011-12-15.png)
```

---

## 十、在 Obsidian 中自动上传图片

仅仅配置 PicGo 还不够。如果想让 Obsidian 里的本地图片自动上传到图床，并替换成网络链接，还需要 Obsidian 插件配合。

推荐插件：

```text
Image auto upload Plugin
```

![PixPin_2026-06-29_11-37-33.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-37-33.png)

它可以配合 PicGo 使用，实现：

```text
粘贴图片自动上传
拖拽图片自动上传
批量上传当前 Markdown 文件中的所有本地图片
上传后自动替换成本地 Markdown 中的图床链接
```

安装方式：

```text
Obsidian → 设置 → 第三方插件 → 浏览 → 搜索 Image auto upload Plugin → 安装并启用
```

![PixPin_2026-06-29_11-40-08.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-06-29_11-40-08.png)

PicGo下载地址：
https://github.com/Molunerfinn/PicGo/releases

---

## 十一、开启 PicGo Server

Image auto upload Plugin 通常通过 PicGo Server 调用 PicGo 上传图片。

打开 PicGo，进入：

```text
PicGo → 设置 → 设置 Server
```

开启 Server。

默认端口一般是：

```text
36677
```

Obsidian 插件中填写：

```text
http://127.0.0.1:36677/upload
```

注意：

```text
使用 Obsidian 上传图片时，PicGo 需要保持运行
PicGo Server 需要保持开启
端口需要和插件里填写的一致
```

---

## 十二、批量上传并替换本地图片

如果一篇文章已经写好了，里面有很多本地图片，可以使用插件的批量上传功能。

操作步骤：

```text
1. 打开需要处理的 Markdown 文件
2. 按 Ctrl + P 打开命令面板
3. 搜索 upload all images
4. 执行命令
5. 等待插件上传图片并替换链接
```

执行前，文章里的图片可能是：

```markdown
![[Pasted image 20260629111215.png]]
```

或者：

```markdown
![](attachments/PixPin_2026-06-29_11-12-15.png)
```

执行后，会变成：

```markdown
![](https://obsidian-image-bed-1251234567.cos.ap-guangzhou.myqcloud.com/Obsidian/20260629111215.png)
```

这样 Markdown 中引用的本地图片就全部替换成了图床链接。

---

## 十三、推荐的最终工作流

我的最终工作流是：

```text
1. 在 Obsidian 中正常写文章
2. 粘贴截图或插入本地图片
3. 使用 Image auto upload Plugin 自动上传图片
4. 或者在写完后执行 upload all images
5. 本地图片链接自动替换成腾讯云 COS 图床链接
6. 检查图片是否能正常显示
7. 复制文章到微信公众号、知乎、飞书、排版工具等平台
8. 发布前再检查一遍图片显示情况
```

整体结构如下：

```text
Obsidian
  ↓
Image auto upload Plugin
  ↓
PicGo / PicList
  ↓
腾讯云 COS
  ↓
公网图片链接
  ↓
微信公众号 / 知乎 / 飞书 / 小红书 / Markdown 排版工具
```

---

## 十四、发布到不同平台的注意事项

### 1. 微信公众号

微信公众号不认识 Obsidian 本地图片路径，所以必须先把图片变成公网链接。

使用图床后，复制文章到公众号草稿时，图片可以正常显示。

如果仍然不显示，需要检查：

```text
图片链接是否能在浏览器打开
COS 是否为公有读私有写
图片链接中是否有空格
是否开启了错误的防盗链规则
```

---

### 2. 知乎

知乎对 Markdown 的支持和公众号不同，复制时可能会重新处理图片。

建议先确保图片链接是标准 Markdown 格式：

```markdown
![](https://example.com/image.png)
```

尽量不要使用 Obsidian 特有语法：

```markdown
![[image.png]]
```

也尽量不要使用：

```markdown
![image.png|260](https://example.com/image.png)
```

其中 `|260` 是 Obsidian 的宽度语法，不是标准 Markdown。

---

### 3. 飞书文档

飞书通常支持复制图片和文本，但如果图片是本地路径，也可能失效。

使用 COS 图床链接后，兼容性更好。

---

### 4. Markdown 排版工具

例如 mdnice、doocs 等 Markdown 排版工具，本质上需要能访问图片的公网 URL。

因此推荐使用标准写法：

```markdown
![](https://your-bucket.cos.ap-guangzhou.myqcloud.com/Obsidian/example.png)
```

---

## 十五、建议保留的配置模板

### 腾讯云 COS 配置模板

```text
Bucket：你的完整 Bucket，例如 obsidian-image-bed-1251234567
APPID：你的 APPID，例如 1251234567
Region：你的地域，例如 ap-guangzhou
访问权限：公有读私有写
存储路径：Obsidian/
```

### PicGo 配置模板

```text
图床类型：腾讯云 COS
SecretId：你的 SecretId
SecretKey：你的 SecretKey
AppId：你的 APPID
Bucket：你的完整 Bucket
Region：你的地域
Path：Obsidian/
Custom URL：留空
```

### Obsidian 插件配置模板

```text
插件：Image auto upload Plugin
PicGo Server：http://127.0.0.1:36677/upload
批量上传命令：upload all images
```

---

## 十六、常见问题总结

### 1. 上传成功，但图片无法显示

优先检查：

```text
1. COS 访问权限是否为公有读私有写
2. 图片链接能否在浏览器直接打开
3. Bucket 和 Region 是否填写正确
4. 图片文件名是否包含空格
5. 是否开启了防盗链
```

---

### 2. Obsidian 中不显示图片

可以把链接改成标准 Markdown 格式测试：

```markdown
![](https://your-image-url.png)
```

不要一开始使用 Obsidian 的宽度语法：

```markdown
![image.png|260](https://your-image-url.png)
```

先确认标准 Markdown 可以显示，再处理图片大小。

---

### 3. 批量上传失败

检查：

```text
1. PicGo 是否正在运行
2. PicGo Server 是否开启
3. 端口是否为 36677
4. Obsidian 插件中的 Server 地址是否正确
5. 腾讯云 COS 密钥是否正确
6. Bucket / APPID / Region 是否正确
```

---

### 4. 是否需要开启 CDN？

个人图床初期不建议开启 CDN。

原因是：

```text
1. 配置更复杂
2. 费用结构更复杂
3. 容易引入缓存、防盗链、域名备案等问题
```

先直接使用 COS 默认域名即可。

---

### 5. 是否需要开启防盗链？

刚开始不建议开启。

如果开启防盗链，白名单配置错误可能导致微信公众号、知乎、飞书或 Markdown 排版工具无法显示图片。

建议先保持默认，等图床稳定使用后再考虑防盗链规则。

---

## 十七、最终效果

配置完成后，Obsidian 中的文章可以从这种本地图片引用：

```markdown
![[Pasted image 20260629111215.png]]
```

变成这种公网图片引用：

```markdown
![](https://obsidian-image-bed-1251234567.cos.ap-guangzhou.myqcloud.com/Obsidian/20260629111215.png)
```

这样，无论是复制到微信公众号、知乎、飞书，还是复制到 mdnice、doocs 等 Markdown 排版工具，图片都不再依赖本地文件，而是通过腾讯云 COS 图床正常加载。

这套方案解决的核心问题是：

```text
让 Obsidian 里的本地图片变成可跨平台访问的公网图片链接。
```

最终，我可以继续在 Obsidian 里保持原来的 Markdown 写作习惯，同时又能比较顺畅地把文章发布到多个平台。