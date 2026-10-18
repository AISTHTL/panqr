# 我让 AI 接管了我的公众号：从接入到一键发文全流程实录

[![封面](https://yulianyanxi.top/assets/up/1792307579162_tut_cover.png)](https://yulianyanxi.top/project.html?id=p-autopub)

<sub>📖 官网图文版（含内嵌视频）：<a href="https://yulianyanxi.top/project.html?id=p-autopub">yulianyanxi.top</a>　|　📚 返回目录：<a href="./../README.md">文章列表</a></sub>

> 作者：橙絮鸢（余恋研喜）
> 关键词：WorkBuddy、公众号自动化、GitHub、一键发文、AI 工作流
> 实录时间：2026 年 10 月 15 日晚，全流程当晚跑通

---

先看结果。

我的公众号后台，草稿箱里那篇文章的创建人一栏，写的不是我的名字，是 **API**。当晚 22:52，群发成功。

![公众号后台：近期发表 今天22:52](https://yulianyanxi.top/assets/up/1792307585746_tut_off_home_published.png)

同一个晚上，我的 GitHub 仓库也是它自己建的、自己推的——README、配图、教程文档，一次到位。

![GitHub 仓库成品 + AI 的三点复盘](https://yulianyanxi.top/assets/up/1792307592109_tut_gh_repo_done.png)

而我做的，只是对 AI 说了一句话：**「把这篇官网文章，发到公众号和 GitHub。」**

这篇文章就把「从接入到自动发文」的全过程拆给你看——包括中间踩过的每一个坑。坑比流程值钱，建议看完。

## 一、现在的发文流程长什么样

以前发一篇文章，我要干五件事：起标题、贴正文、传图片、设封面、挂原文链接，一套下来二十分钟没了。现在我只需要两步：

1. 文章先发到自己官网（这一步 AI 也包了）；
2. 对 WorkBuddy 说：「把这篇发到公众号」。

然后大约十分钟，打开公众号后台「内容与互动 → 草稿箱」，文章已经在里面躺着了——标题、作者、摘要、封面、正文配图全部就位，「创建人」一栏写着 API，证明它是接口推进来的，不是我手动贴的。

![草稿箱里的文章，创建人是 API](https://yulianyanxi.top/assets/up/1792307585043_tut_off_draft_api.png)

我打开预览，确认排版没问题，点群发。**最后一步永远留给人**——AI 推草稿，人按发射键，这样既省事又不会误发。

## 二、整体设计：一篇文章，三个渠道

我的内容分发是「一源三渠道」：

- **官网（源）**：文章、图片、视频全部先放在自己网站，地址自己可控，随时能改；
- **公众号（流量）**：同一篇内容输出两种形态——长图文 + 贴图（小绿书），贴图吃推荐流量，图文沉淀信任；
- **GitHub（存档）**：Markdown 版 + 原始文档进仓库，公开可引用，也当内容备份。

为什么官网是源？因为公众号不支持外链图片，GitHub 上图片托管也麻烦，而自己网站上的资源，三个渠道都能随便引用。**先把源站建好，自动化才有地基。**

## 三、准备工作：三样东西

| 准备 | 说明 |
|---|---|
| 一个公众号 | 企业/个体户主体最好，接口权限全；个人订阅号也够用 |
| 一台云服务器 | 公众号接口只认白名单 IP，脚本必须放在固定 IP 的服务器上跑 |
| WorkBuddy（AI 助手） | 负责所有脏活：格式转换、传图、调接口、推草稿 |

服务器不用贵的，轻量的就够——它只干一件事：替你调用微信和 GitHub 的接口。

## 四、第一步：接入公众号接口

### 卡点一：开发者入口整个没了

我信心满满打开公众号后台找「开发接口管理」，结果翻了个遍——入口没了。只剩一张通知：《开发管理模块迁移通知》。

![公众号后台只剩一张迁移通知](https://yulianyanxi.top/assets/up/1792307580586_tut_off_migration.png)

<p align="center">
  <a href="https://yulianyanxi.top/assets/up/1792307611073_tut_v_migration.mp4"><img src="https://yulianyanxi.top/assets/up/1792307580586_tut_off_migration.png" alt="后台翻不到开发者入口" width="640"></a><br>
  <a href="https://yulianyanxi.top/assets/up/1792307611073_tut_v_migration.mp4"><b>▶ 点击播放：后台翻不到开发者入口</b></a>
</p>

点开官方文档才知道：从 2025 年 12 月起，AppID/AppSecret 这些开发密钥**全部迁到了「微信开发者平台」**，公众号后台不再保留。第一次接公众号接口的人，十个有九个在这懵住。

![微信官方迁移说明文档](https://yulianyanxi.top/assets/up/1792307581223_tut_off_doc.png)

**解法：** 打开 [developers.weixin.qq.com/platform](https://developers.weixin.qq.com/platform/)（微信开发者平台），用**管理员微信**扫码登录，在「我的业务 → 公众号 → 基础信息」里找到开发密钥。

![微信开发者平台](https://yulianyanxi.top/assets/up/1792307581898_tut_off_devplatform.png)

### 拿两样东西：AppID 和 AppSecret

- **AppID**：明摆着，直接抄；
- **AppSecret**：要点「生成/重置」，管理员扫码后**只显示一次**，弹窗一关再也找不回来——复制了立刻存好。

![开发者平台：生成 AppSecret](https://yulianyanxi.top/assets/up/1792307582546_tut_off_secret.png)

<p align="center">
  <a href="https://yulianyanxi.top/assets/up/1792307612694_tut_v_secret.mp4"><img src="https://yulianyanxi.top/assets/up/1792307582546_tut_off_secret.png" alt="开发者平台取密钥" width="640"></a><br>
  <a href="https://yulianyanxi.top/assets/up/1792307612694_tut_v_secret.mp4"><b>▶ 点击播放：开发者平台取密钥</b></a>
</p>

### 卡点二：40164，接口直接拒了你

拿到密钥一调接口，报错 `40164 invalid ip`——微信要求调用方 IP 必须在白名单里。解法：还是在「开发密钥」区域，把**API IP 白名单**配上你云服务器的公网 IP，保存。

这就是为什么准备清单里有台服务器：**发文脚本全部放在服务器上跑**，IP 固定，白名单一次配好再也不动。

### 密钥放哪：服务器，本地不留底

AppSecret 相当于公众号的钥匙。我的做法是：**明文只存在云服务器的配置文件里**（权限设 600，仅服务器自己可读），本地电脑、笔记、代码仓库一概不留。万一哪台设备被盗，也盗不走这把钥匙。

## 五、第二步：自动发文跑通（图文）

### 文章怎么交给 AI

我的文章先发在官网。然后我对 WorkBuddy 说一句：「官网这篇，直接推到我的公众号。」

![官网文章页：自动化的源头](https://yulianyanxi.top/assets/up/1792307579927_tut_off_article_page.png)

### AI 干的活：格式转换 + 图片自动传素材库

这里有个铁律：**公众号图文不认外链图片**。你正文里写 `https://你的网站/图.png`，微信会直接吞掉不显示。

AI 的处理方式是把正文里每一张图**自动上传到公众号素材库**，换成微信内部的 media_id 再塞回正文，最后调 `draft/add` 接口把整篇文章推进草稿箱。十分钟后，草稿箱见——就是开头截图里那篇「创建人 API」。

### 卡点三：视频塞不进图文

实测发现：`draft/add` 接口的正文 HTML **无法嵌入视频**，不管是外链视频还是素材库视频，API 都拿不到可播放地址。这是平台限制，不是 bug。

AI 的解法分两步：

1. 它先把视频**自动传进公众号素材库**（接口支持上传视频）：

![视频已传进素材库](https://yulianyanxi.top/assets/up/1792307584281_tut_off_material_video.png)

2. 草稿推过来时，在视频该出现的位置放一个醒目提示框。我打开草稿，点编辑器的「视频 → 素材库 → 选中 → 插入」，两秒钟的事，然后把提示框删掉。

![编辑器插入视频](https://yulianyanxi.top/assets/up/1792307583272_tut_off_video_popup.png)

<p align="center">
  <a href="https://yulianyanxi.top/assets/up/1792307616876_tut_v_video_insert.mp4"><img src="https://yulianyanxi.top/assets/up/1792307583272_tut_off_video_popup.png" alt="视频插入实录" width="640"></a><br>
  <a href="https://yulianyanxi.top/assets/up/1792307616876_tut_v_video_insert.mp4"><b>▶ 点击播放：视频插入实录</b></a>
</p>

所以带视频的文章，自动化程度是 99%：**AI 包揽所有上传和排版，人只点两下插入视频**。

### 摘要、原文链接、赞赏

草稿里的摘要 AI 会按文章内容自动生成，我可以改；原文链接默认指向官网文章页——公众号文章的流量就能导回自己网站。顺手把**赞赏**也开了，这些都是公众号自带的功能，不开白不开。

![编辑摘要](https://yulianyanxi.top/assets/up/1792307587041_tut_off_summary.png)

## 六、顺手一条「贴图」（小绿书）

意外收获：同一篇文章，AI 还能顺手浓缩成一条**贴图**——就是「小绿书」，三到九张图配短文案，形态几乎就是小红书笔记。

微信的草稿接口原生支持贴图类型（`article_type: newspic`），所以这一步也是全自动：收益截图当首图（自动成封面），后面跟着海报、工具截图，文案 AI 浓缩，赞赏和原文链接的设置位都给你留好。

![贴图编辑器：赞赏、原文链接位置都留好了](https://yulianyanxi.top/assets/up/1792307586406_tut_off_newspic.png)

贴图吃的是公众号的推荐流量，官方数据说平均阅读比长图文高好几倍。**长图文拉信任，贴图拉新**，一篇文章两条内容，发布时挨个点群发就行。

## 七、第四步：同步挂上 GitHub

### 三样准备：用户名、仓库名、token

GitHub 这边，AI 开口就要三样：你的 GitHub 用户名、想建的仓库名，还有一个 **Personal Access Token**——访问钥匙。

![GitHub 主页 + AI 列出的准备清单](https://yulianyanxi.top/assets/up/1792307587730_tut_gh_home.png)

领钥匙的路径：头像 → Settings → 拉到最底 → Developer settings → Personal access tokens。生成前 GitHub 会要你**再输一遍密码**确认身份——别嫌烦，防的就是钥匙被人顺走。

![个人资料页](https://yulianyanxi.top/assets/up/1792307588668_tut_gh_profile.png)

![Confirm access：输密码确认](https://yulianyanxi.top/assets/up/1792307589451_tut_gh_confirm.png)

### 卡点四：新式 token 报 403

我第一次生成的是 GitHub 新出的 **fine-grained（细粒度）token**，看着高级，权限能精确到每个仓库。结果 AI 那边一跑——403，没有建仓权限。这把新钥匙开不了「创建仓库」这扇门。

![fine-grained token 权限页](https://yulianyanxi.top/assets/up/1792307590117_tut_gh_finegrained.png)

**解法老套但管用：换回 classic token**。Note 随便写个名字，权限勾 **repo**（建仓+推送就靠这一项），生成。注意 scope 千万别勾漏——勾漏了后面直接 404。

![classic token：勾 repo](https://yulianyanxi.top/assets/up/1792307590798_tut_gh_classic.png)

<p align="center">
  <a href="https://yulianyanxi.top/assets/up/1792307618378_tut_v_classic_token.mp4"><img src="https://yulianyanxi.top/assets/up/1792307590798_tut_gh_classic.png" alt="classic token 生成实录" width="640"></a><br>
  <a href="https://yulianyanxi.top/assets/up/1792307618378_tut_v_classic_token.mp4"><b>▶ 点击播放：classic token 生成实录</b></a>
</p>

### 卡点五：空仓库 404 + clone 挂起

仓库建好了，打开直接 404？**别慌，这不是翻车**——空仓库本来就没有页面，推完文件自然就有了。

真正麻烦的是推送：服务器上 `git clone` GitHub 会莫名挂起。AI 的处理是不走寻常路——直接调 GitHub 的 **Contents API**，把文件从服务器端一个 PUT 写进 main 分支，空仓库的第一个提交就这么成了。

### 成品

刷新页面：README（图文完整渲染）、原始教程文档，全在。

<p align="center">
  <a href="https://yulianyanxi.top/assets/up/1792307621798_tut_v_repo_done.mp4"><img src="https://yulianyanxi.top/assets/up/1792307592109_tut_gh_repo_done.png" alt="GitHub 仓库成品" width="640"></a><br>
  <a href="https://yulianyanxi.top/assets/up/1792307621798_tut_v_repo_done.mp4"><b>▶ 点击播放：GitHub 仓库成品</b></a>
</p>

## 八、卡点速查表

把这一晚踩的坑浓缩成一张表，你接的时候照着绕：

| # | 卡点 | 现象 | 解法 |
|---|---|---|---|
| 1 | 开发者入口消失 | 后台只剩迁移通知 | 去 developers.weixin.qq.com/platform 取密钥 |
| 2 | 接口报 40164 | invalid ip | 服务器 IP 加进 API IP 白名单，脚本放服务器跑 |
| 3 | 图片不显示 | 外链图被吞 | 图片必须上传素材库换 media_id |
| 4 | 视频嵌不进图文 | API 拿不到视频地址 | 视频传素材库，编辑器手动点两下插入 |
| 5 | GitHub 403 | fine-grained token 没建仓权限 | 换 classic token，勾 repo |
| 6 | GitHub 404 | scope 勾漏 / 空仓库 | 重新生成勾齐 repo；空仓库 404 是正常现象 |
| 7 | 服务器 clone 挂起 | git 推送超时 | 改用 GitHub Contents API 直推 |

## 九、日常怎么用，以及安全底线

**日常**：文章写好发官网 → 一句「把这篇发到公众号 / GitHub」→ 十分钟后草稿箱见 → 手机预览 → 群发。我碰键盘的时间不到三分钟。

**安全底线，四条：**

1. **AppSecret 只存服务器**，本地、笔记、仓库不留明文；泄露就去开发者平台重置，重置后更新服务器配置即可；
2. **GitHub token 有有效期**，到期或用完就去删掉重发——钥匙用完就换，这是规矩；
3. **最后一步永远人工**：AI 只推草稿，群发的按钮永远自己按，防误发；
4. 素材发布前做合规自查：密钥不入镜、隐私内容不出现。

## 写在最后

这套流程搭建的当晚，我同时完成了：公众号长图文一篇、贴图一条、GitHub 仓库一个。以前这是一晚上的活，现在是三句话的事。

技术门槛其实不高——难的都是那种「没人告诉你就会卡一晚上」的坑，比如迁移后的密钥入口、40164、403、空仓库 404。这篇文章把坑都摆在桌上了，你照着走，一次通。

如果你想让我帮你搭这套流程，或者对某个步骤有疑问，公众号后台留言，或者来官网 [yulianyanxi.top](https://yulianyanxi.top) 找我。

---

---

*本文由橙絮鸢（余恋研喜）实录、AI 协助整理。首发于 [yulianyanxi.top](https://yulianyanxi.top/project.html?id=p-autopub)。转载请注明出处。*
