# claude-skill-taobao-store-designer

**淘宝店铺首页设计 Claude Skill** — 品牌配置驱动，模块化组合，导出 1200px 图片直接上传千牛。

A Claude skill for designing Taobao store homepages — brand-configurable, modular, exports 1200px images ready for Qianniu upload.

---

## 它能做什么 / What it does

安装后，这个 Skill 会引导 Claude 走一套三步工作流：

1. **收集品牌信息** — 品牌名、品类、风格关键词、色彩偏好、需要哪些模块
2. **输出方案摘要** — 色彩方案、模块顺序、排版变体选择、视觉串联方式，等你确认
3. **生成单文件 HTML 编辑器** — 在浏览器里直接改文字、换图片，导出全套 1200px PNG

Once installed, the skill guides Claude through a 3-step workflow: collect brand info → propose a design plan (wait for confirmation) → generate a single-file HTML editor for in-browser editing and 1200px export.

导出的图片按千牛模块顺序命名，直接上传对应模块即可。

---

## 千牛模块对应关系 / Qianniu Module Map

| 千牛模块 | 需要上传的图 | 导出尺寸 |
|---|---|---|
| 轮播图海报 | 每张 Banner 独立导出 | 1200 × 600px |
| 单图海报 | 系列头图、过渡图、品牌故事 | 1200 × 任意高 |
| 多热区切图 | 分类导航图 | 1200 × 480px |
| 店铺优惠券 | 不需要图，千牛原生模块 | — |
| 系列主题宝贝 | 不需要图，千牛原生模块 | — |

---

## 编辑器功能 / Editor Features

- **文字直接编辑** — 点击任意文字，光标进入，打字修改
- **图片一键替换** — 鼠标悬停图片区域 → 点击上传产品图/模特图
- **模块自由排序** — 悬停模块右上角出现：上移 / 下移 / 单独导出 / 删除
- **左侧面板随时添加模块** — 可在任意位置插入新模块

**三种导出方式：**
- 单模块导出 → 输出 `品牌名_模块名_1200px.png`
- ZIP 打包 → 全部模块一次下载，不弹多次确认
- 合并长图 → 所有模块垂直拼合成一张完整首页图

所有图片自动压缩到 2MB 以内。 / All exports are automatically compressed to stay under 2MB.

---

## 设计系统 / Design System

### 模块排版变体 / Layout Variants

每种模块有多种排版，Claude 根据品牌风格选择，相邻同类模块使用不同变体避免重复感。

Each module type has multiple layouts. Claude picks based on brand style and alternates variants to avoid repetition.

**Banner / Hero**
- A 全出血 / Full-bleed：图铺满，渐变遮罩，文字叠底左
- B 分屏 / Split screen：左图右文，背景色衬底
- C 留白居中 / Centered：图约 60% 宽居中，四周大量留白

**系列展示 / Series Showcase**
- A 标题溢出 / Overflow title：系列名从上方区块延伸压住图片
- B 左图右文 / Left photo right text
- C 右图左文 / Right photo left text（与 B 交替）
- D 全出血竖排 / Full-bleed vertical type

**过渡条 / Divider**
- A 细线夹字：`——— SERIES ———`
- B 大字锚点：超大透明背景字 + 前景编号
- C 纯色块：整行换背景色

**分类导航 / Category Nav**
- A 等高四格 / Equal columns
- B 错落高度 / Staggered heights（高-矮-高-矮）
- C 横向文字条 / Text-only strips

**品牌故事 / Brand Story**
- A 左图右文 / Photo left text right
- B 大引语居中 / Large centered quote
- C 深色全出血 / Dark full-bleed

### 背景色策略 / Background Strategy

**关键洞察 / Key insight**：近白或白色背景让模块边界消失，页面读起来像一个整体而不是拼凑的块。Near-white backgrounds make module boundaries disappear — the page reads as one continuous scroll.

| 品牌风格 / Style | 推荐背景 / Background |
|---|---|
| 极简 / 现代 | 近白 `#F8F6F3` ↔ `#EEEAE4` |
| 中式 / 手工艺 | 暖亚麻 `#EAE0CC` ↔ `#DDD2BA` |
| 高级 / 暗黑 | 深墨 `#1C1814` ↔ `#2A2520` |
| 活泼 / 清新 | 品牌色 + 白色卡片交替 |

### 字体预设 / Font Presets

字体通过品牌配置对象管理，不写死，Claude 根据风格选择。

Fonts are managed via brand config — not hardcoded. Claude picks from presets based on style keywords.

| 风格 / Style | 中文 / Chinese | 英文 / English |
|---|---|---|
| 高级感 / 珠宝 | Noto Serif SC | Cormorant Garamond italic |
| 活泼 / 国潮 | ZCOOL KuaiLe | DM Sans |
| 户外 / 工装 | Noto Sans SC | Space Grotesk |
| 复古 / 中式 | ZCOOL XiaoWei | Playfair Display |
| 现代 / 科技 | Noto Sans SC | Inter |
| 手工艺 / 生活 | Ma Shan Zheng | Lora |

---

## 安装方法 / Installation

### Claude Desktop

1. 下载 / Download `taobao-store-designer.skill`
2. 打开 Claude Desktop → 进入你的 Project → Settings
3. 在 Skills 区域上传 `.skill` 文件

安装后，在该 Project 的任何对话里提到 **「淘宝首页」「店铺装修」「千牛」** 或 **"store homepage"**，Claude 会自动读取这个 Skill，按三步工作流执行。

After installation, mention **"淘宝首页"**, **"千牛"**, **"店铺装修"**, or **"store homepage"** in any conversation in that project to trigger the workflow.

### 查看 Skill 源码 / View Source

`.skill` 文件本质是 ZIP 压缩包，改后缀为 `.zip` 解压，里面是 `SKILL.md`。

The `.skill` file is a ZIP archive. Rename to `.zip` and extract to read `SKILL.md`.

---

## 技术说明 / Technical Notes

以下是这套方案经过迭代验证的几个关键技术决策：

**`background-image` 而不是 `<img>`**
html2canvas 不支持 `object-fit: cover`，用 `<img>` 导出必然变形。所有图片区使用 CSS `background-image` + `background-size: cover`。
*html2canvas does not support `object-fit: cover`. All image zones use `background-image` instead of `<img>`.*

**禁止 `innerHTML +=`**
`innerHTML +=` 会序列化重建 DOM，销毁已有节点的事件监听器，导致换图失效。全部用 `createElement` + `appendChild`。
*`innerHTML +=` destroys event listeners on existing nodes. Always use `createElement` + `appendChild`.*

**iframe 隔离确保真实 1200px 导出**
画布预览通过 CSS `transform: scale(0.325)` 缩小到 390px 显示。导出时把模块写入隐藏 iframe，在 iframe 内以真实 1200px 渲染后截图。
*The preview scales the 1200px design down via CSS transform. Export renders each module inside a hidden iframe at true 1200px.*

**`document.fonts.ready` 等待字体**
Google Fonts 异步加载，固定延时不可靠。用 `iDoc.fonts.ready` 确保字体实际可用后再截图。
*Use `iDoc.fonts.ready` instead of a fixed timeout to ensure fonts are actually loaded before capture.*

**高度稳定检测后再截图**
`min-height` 的模块高度动态撑开。导出前等待 `scrollHeight` 连续 3 次相同，确认稳定。
*Wait for `scrollHeight` to be identical 3 times in a row before capturing, to handle dynamically expanding modules.*

**合并长图逐个释放内存**
每个模块截图后立刻转为 dataURL 释放 canvas。合并时用 `Image` 对象绘制，避免多个大 canvas 同时占用内存。
*Convert each canvas to dataURL immediately after capture, then assemble with `Image` objects to avoid OOM.*

---

## 已知限制 / Known Limitations

- 千牛自定义 HTML 模块不支持 JavaScript，所有导出为静态图片 / Qianniu does not support JS in custom HTML modules — all outputs are static images
- 新版淘宝通用货品店的店招背景由系统控制，不支持自定义图片 / The store header background is system-controlled in new Taobao stores and cannot be customized

---

## License

MIT
