<!--
GitHub 版发布说明：
1. 推送前把下面所有 {{IMG_xxx}} 占位符替换为图床公网 URL
   （官网图床接口走 RAW BODY 方式上传，上传后把返回 URL 逐一替换）。
2. 视频块：把 https://yulianyanxi.top/assets/up/1793261370665_1029__41af40.mp4 换成视频公网直链（如官网/网盘直链）。
3. 推送命令（需 GH_TOKEN + GH_REPO）：
   export GH_TOKEN=ghp_xxx GH_REPO=用户名/仓库名
   python3 scripts/gh_push_article.py put articles/NN-house-plan-designer.md 本文.md "docs: 新增"
-->

# 上传一张户型图，先"走进"新家看看：这个 AI 装修设计器我实测了

<p align="center"><a href="https://yulianyanxi.top/assets/up/1793261370665_1029__41af40.mp4"><img src="https://yulianyanxi.top/assets/up/1793261355550_cover_house_designer_16x9_db18fa.png" width="640"></a><br><a href="https://yulianyanxi.top/assets/up/1793261370665_1029__41af40.mp4"><b>▶ 点击播放：完整实操演示（10月29日.mp4）</b></a></p>

**装修最怕的不是花钱，是想象不出来。** 中介发的户型图是平的，装修公司的效果图是"仅供参考"。这次我把一个户型图丢给 AI，得到一个**能漫游、能摆家具、能规划水电、能出报价和施工图的 3D 装修设计器网页**。

## 一、这是个什么东西

它叫 house-plan-designer（户型装修设计器）。玩法一句话：

**上传一张户型图 → AI 自动识别房间、门窗、墙体 → 帮你布置家具和水电 → 生成一个能直接打开的单文件 HTML。**

## 二、实测：从一张图到能走进的房子

- **19 面墙自动识别**，识别完可与原图叠加校验
- 识别结果：**33 面墙 / 15 个门窗 / 8 个房间**
- 底部状态栏实时显示**套内净面积 90.29 ㎡**（自己拿计算器核过，对的）

| 识图分析 | 2D 全景 |
|---|---|
| ![](https://yulianyanxi.top/assets/up/1793261356831___de584f.png) | ![](https://yulianyanxi.top/assets/up/1793261354787_ui_01_2D_55a848.png) |

## 三、3D 漫游：装修前先"走进"新家

3D 鸟瞰整套房一览无余；点「漫游」WASD 走两步，1.60m 视高，从客厅走进走廊。拖家具时右侧坐标、尺寸、所在房间实时变。

| 3D 鸟瞰 | 漫游视角 |
|---|---|
| ![](https://yulianyanxi.top/assets/up/1793261354947__3D_4d1b03.png) | ![](https://yulianyanxi.top/assets/up/1793261356645_ui_05__349861.png) |

## 四、水电一键布置 + 它会"挑毛病"

一键布置水电自动生成 **63 个点位 / 11 个开关 / 25 个插座 / 8 盏灯**；强电、开关、灯具、弱电、给水、燃气分组查看导出。

检查面板当场列问题（工具原话）：

> - ⚠️ **门被挡住**：餐椅挡住了「客餐厅 / 次卧」之间的门，门扇打不开
> - ⚠️ **通道不足**：从入户门到「阳台 / 客餐厅」的门，没有净宽 ≥ 700mm 的通道
> - 💡 **遮挡窗户**：淋浴房 高 2,000mm，挡住了窗户

| 一键水电 | 检查提醒 |
|---|---|
| ![](https://yulianyanxi.top/assets/up/1793261355736_08__7494fe.png) | ![](https://yulianyanxi.top/assets/up/1793261356492_07__01d33b.png) |

## 五、算量报价 + 施工图导出

报价清单按房间自动算量，可导出 CSV；导出图纸菜单实测 **10 项**（A3 施工图 PDF / 平面布置 / 地面铺装 / 顶面布置 / 水电点位 / 拆改图 / 彩平 PNG 等）。另有日照演示、一键夜景亮灯、12 套配色风格切换。

| 报价面板 | 导出菜单 |
|---|---|
| ![](https://yulianyanxi.top/assets/up/1793261356175_ui_06__79eeea.png) | ![](https://yulianyanxi.top/assets/up/1793261355901_ui_07__b394d0.png) |

## 六、怎么装怎么用

1. 把 Skill 地址或压缩包发给 WorkBuddy，在项目空间安装
2. 选中调用这个 Skill，上传你的户型图
3. 说一句：**"把这个户型做成装修设计器网页"**

正准备装修或买房的话，真的建议先用它试着规划布局——**先把想法摆进空间里，装修决定才更容易看清楚。**

---

*本文由橙絮鸢（余恋研喜）实录、AI 协助整理。首发于 [yulianyanxi.top](https://yulianyanxi.top/project.html?id=p-autopub)。转载请注明出处。觉得有用的话，欢迎关注公众号 **橙絮鸢**，持续分享 AI 实战。*
