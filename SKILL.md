---
name: taobao-store-designer
description: |
  Design and generate Taobao (淘宝) store homepage module images for upload to Qianniu (千牛) store decoration. Use this skill whenever a user wants to:
  - Design a Taobao/淘宝 store homepage (首页装修)
  - Create store banner images, series showcases, category navigation, or brand story sections
  - Build a modular store design tool in HTML that exports 1200px images
  - Design e-commerce product showcase pages for Chinese platforms
  - Create a customizable store template for different brands
  Always use this skill when "淘宝", "千牛", "店铺装修", "首页", "Banner", or "store homepage" are mentioned alongside design or image generation requests.
---

# Taobao Store Homepage Designer

## 工作流程（严格按顺序执行）

### ⚠️ 强制规则：无论是否认识该品牌，必须先完成第一轮问答再生成任何代码

即使用户提到了知名品牌（如 Snow Peak、Nike、优衣库、lululemon），也**禁止**用训练数据里的品牌信息替代用户的实际输入。用户可能需要的是「风格参考该品牌，但内容完全自定义」的版本。跳过问答直接生成是错误的。

---

### 第一步：收集品牌信息

一次性发出所有问题，不要分多轮：

```
我来帮你设计淘宝首页，先了解几个基本信息：

1. 品牌名称（中英文各一个）
2. 卖什么品类？
3. 品牌风格关键词（选 2-3 个）：
   极简 / 复古 / 中式 / 活泼 / 高级感 / 自然 / 暗黑 / 甜美 / 工装 / 清新
4. 有哪些系列或分类？（首页会按系列或按品类来组织）
5. 有没有品牌色偏好？（没有的话我来推荐）
6. 首页需要哪些模块？（默认：Banner + 优惠券 + 系列展示 + 分类导航 + 品牌故事）
```

### 第二步：输出方案摘要，等用户确认

```
## 首页方案

**品牌**：[名称] / [英文]
**风格定位**：[关键词]

**色彩**：
- 主背景：[色值] — [一句话说明，例如：近白色让模块边界消失，更有整体感]
- 文字：[色值]
- 点缀：[色值]

**模块组合**：
[按顺序列出，每个模块说明用的是哪种排版变体，以及为什么选这个变体]

**视觉串联**：[描述贯穿全页的元素，例如：金色细线 + 各区块超大水印字]

确认以上方案，我就开始生成 HTML 编辑器。有需要调整的也可以告诉我。
```

### 第三步：生成 HTML 编辑器

用户确认后，生成完整的单文件 HTML，包含：
- 左侧面板：添加/排序模块的按钮
- 中间画布：390px 缩放预览
- 文字全部 `contenteditable`，点击直接改
- 图片区点击可替换
- 导出：单模块 / ZIP 打包 / 合并长图，均输出 1200px

---

## 模块库与排版变体

**同一个页面里，相邻的同类模块必须使用不同的排版变体。**

### Banner / Hero 区

| 变体 | 构图 | 适合 |
|---|---|---|
| A 全出血 | 图 `position:absolute;inset:0` 铺满，渐变遮罩，文字绝对定位叠底左 | 有强视觉冲击的产品图 |
| B 分屏 | 左图右文（或左文右图），各占宽度，背景色衬底 | 产品图不够强，文字内容多 |
| C 留白居中 | 图片宽度约 60%，水平居中，四周大量留白 | 极简高端感 |

### 系列展示区

| 变体 | 构图 | 适合 |
|---|---|---|
| A 标题溢出 | 系列名从上方区块底部延伸，压住图片顶部 30–50px | 打破模块感，连续性强 |
| B 左图右文 | 55% 图 + 45% 文字面板 | 有内容要讲的系列 |
| C 右图左文 | 45% 文字面板 + 55% 图（与 B 交替） | 和上一系列形成对称节奏 |
| D 全出血竖排 | 图铺满，文字竖排叠在左/右侧 | 有调性的大图 |

### 过渡 / 锚点区

| 变体 | 构图 |
|---|---|
| A 细线夹字 | `——— 系列名 ———` 水平排列 |
| B 大字锚点 | 背景超大透明字，前景编号+系列名 |
| C 纯色块 | 整行换背景色，宽度铺满 |

### 分类导航区

| 变体 | 构图 |
|---|---|
| A 等高四格 | 4 列等宽等高，交替浅色 |
| B 错落高度 | 高-矮-高-矮 交替 |
| C 横向文字条 | 纯文字横排，右对齐英文 |

### 品牌故事区

| 变体 | 构图 |
|---|---|
| A 图文并排 | 左图 45% + 右文字 55% |
| B 引语居中 | 大引语居中 + 下方图文 |
| C 深色全出血 | 深色背景 + 文字叠图 |

---

## 模块组合原则

**节奏**：不要让同一类构图连续出现。好的节奏示例：
```
Hero（A 全出血）
↓ 过渡条（A 细线夹字）
系列一（A 标题溢出）← 暖色背景
↓ 过渡条（B 大字锚点）
系列二（B 左图右文）← 换深色背景
↓
分类导航（B 错落高度）← 回浅色
↓
品牌故事（C 深色全出血）← 深色收尾
```

**背景交替**：相邻模块用 2–3 个不同深浅背景值。

**视觉串联**（必须有一个）：
- 图案轨迹：SVG 品牌图案沿弧线分布（透明度 15–20%）
- 大字水印：品牌名超大字叠在区块背景（透明度 3–5%）
- 编号节奏：01 / 02 / 03 统一字体/颜色/位置
- 细竖线：左侧 52px 处 1px 虚线 + 节点装饰

**背景色策略**：

| 风格 | 背景 |
|---|---|
| 极简 / 现代 | 近白 `#F8F6F3` ↔ `#EEEAE4`，边界感消失 |
| 中式 / 手工艺 | 暖亚麻 `#EAE0CC` ↔ `#DDD2BA` |
| 高级 / 暗黑 | 深墨 `#1C1814` ↔ `#2A2520` |
| 活泼 / 清新 | 品牌色 + 白色卡片交替 |

---

## 千牛模块对应

| 千牛模块 | 需要图 | 尺寸 |
|---|---|---|
| 轮播图海报 | 每张 Banner 独立导出 | 1200×600px |
| 单图海报 | 系列头图、过渡图、品牌故事 | 1200×任意高 |
| 多热区切图 | 分类导航 | 1200×480px |
| 店铺优惠券 | 不需要，千牛原生模块 | — |
| 系列主题宝贝 | 不需要，千牛原生模块 | — |

---

## 技术规则（生成代码时严格遵守）

### 图片区用 background-image，不用 `<img>`

html2canvas 不支持 `object-fit: cover`，用 `<img>` 导出必变形。

```js
zone.style.backgroundImage = 'url(' + JSON.stringify(dataUrl) + ')';
zone.style.backgroundSize = 'cover';
zone.style.backgroundPosition = 'center';
zone.style.backgroundRepeat = 'no-repeat';
```

**每个图片区必须有占位背景色**，否则上传图片前页面显示空白：
```js
imgZone.style.cssText = '...;background-color:#E8E4DE;';
```

### 禁止 innerHTML += 追加节点

销毁事件监听器，换图失效。

```js
// 错误
block.appendChild(imgZone);
block.innerHTML += '<div>...</div>'; // imgZone 事件被销毁

// 正确：全部 createElement + appendChild
```

### Hero 变体 A 的正确 DOM 结构

图必须 `position:absolute;inset:0` 铺满，文字层用 `position:absolute` 叠上去。

```js
// 容器
db.style.cssText = 'height:600px;position:relative;overflow:hidden;';

// 图片层：铺满
const imgZone = document.createElement('div');
imgZone.style.cssText = 'position:absolute;inset:0;background-color:#E8E4DE;background-size:cover;background-position:center;';
makeUploadable(imgZone);
db.appendChild(imgZone);

// 渐变遮罩（让文字易读）
const overlay = document.createElement('div');
overlay.style.cssText = 'position:absolute;inset:0;background:linear-gradient(105deg,rgba(0,0,0,.4) 0%,transparent 60%);pointer-events:none;z-index:2;';
db.appendChild(overlay);

// 文字层：叠在图上
const textLayer = document.createElement('div');
textLayer.style.cssText = 'position:absolute;bottom:60px;left:88px;z-index:5;';
db.appendChild(textLayer);
```

### 换图用 label 覆盖 input

```js
function makeUploadable(zone) {
  const label = document.createElement('label');
  label.style.cssText = 'position:absolute;inset:0;cursor:pointer;z-index:10;';
  const inp = document.createElement('input');
  inp.type = 'file'; inp.accept = 'image/*';
  inp.style.cssText = 'width:0;height:0;opacity:0;position:absolute;';
  inp.addEventListener('change', e => {
    const r = new FileReader();
    r.onload = ev => {
      zone.style.backgroundImage = 'url(' + JSON.stringify(ev.target.result) + ')';
      zone.style.backgroundSize = 'cover';
      zone.style.backgroundPosition = 'center';
      inp.value = '';
    };
    r.readAsDataURL(e.target.files[0]);
  });
  label.appendChild(inp);
  zone.appendChild(label);
}
```

### mod-wrapper 高度塌陷修法（scale 导致大片空白）

`transform:scale()` 不影响布局空间，必须手动设置 wrapper 高度。

```css
.mod-wrapper {
  position: relative;
  width: 390px;
  overflow: hidden; /* 必须 */
}
.mod-wrapper .db {
  width: 1200px;
  transform-origin: top left;
  transform: scale(0.325);
  display: block;
}
```

```js
// 模块插入后动态设定 wrapper 高度
function updateWrapperHeight(wrapper, db) {
  const h = db.scrollHeight || db.offsetHeight;
  if (h > 0) wrapper.style.height = Math.ceil(h * 0.325) + 'px';
}
requestAnimationFrame(() => updateWrapperHeight(wrapper, db));
setTimeout(() => updateWrapperHeight(wrapper, db), 100);
setTimeout(() => updateWrapperHeight(wrapper, db), 400);
```

---

## 导出函数（必须使用以下完整实现，不能简化）

### renderMod — 单模块渲染为 canvas

**关键点**：
1. 截图前隐藏操作按钮（否则 hover 状态的按钮会被截进图）
2. Google Fonts 用 `<link>` 硬编码写入 iframe，不通过 cssRules 提取（跨域报错会丢失字体样式）
3. 用 `iDoc.fonts.ready` 等待字体加载完成，不用固定 setTimeout
4. 用「高度连续3次相同」判断渲染稳定，再执行截图

```js
async function renderMod(id) {
  const shell = document.getElementById(id);
  const block = shell.querySelector('.db');
  if (!block) return null;

  // 1. 截图前隐藏操作按钮
  const actions = shell.querySelector('.mod-actions');
  if (actions) actions.style.visibility = 'hidden';

  // 2. 提取同源样式（跨域 sheet 会报错，try/catch 跳过）
  const allStyles = Array.from(document.styleSheets).map(ss => {
    try { return Array.from(ss.cssRules).map(r => r.cssText).join('\n'); }
    catch(e) { return ''; }
  }).join('\n');

  // 3. 创建 iframe，硬编码 Google Fonts link
  const iframe = document.createElement('iframe');
  iframe.style.cssText = 'position:fixed;top:-9999px;left:-9999px;width:1200px;height:1px;border:none;z-index:-1;';
  document.body.appendChild(iframe);
  const iDoc = iframe.contentDocument;
  iDoc.open();
  iDoc.write(`<!DOCTYPE html><html><head>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@200;300;400;500&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&display=swap" rel="stylesheet">
    <style>
      html,body{margin:0;padding:0;width:1200px;overflow:visible;}
      ${allStyles}
      .db{transform:none!important;width:1200px!important;}
      .mod-actions{display:none!important;}
    </style>
    </head><body>${block.outerHTML}</body></html>`);
  iDoc.close();

  // 4. 等待字体加载完成（用 fonts.ready，不用固定延时）
  try {
    await iDoc.fonts.ready;
  } catch(e) {
    await new Promise(r => setTimeout(r, 800)); // 兜底
  }

  // 5. 等待高度稳定（连续3次 scrollHeight 相同才开始截图）
  const inner = iDoc.querySelector('.db');
  await waitForStableHeight(inner);
  const realH = inner.scrollHeight;
  iframe.style.height = realH + 'px';
  await new Promise(r => setTimeout(r, 80));

  let canvas = null;
  try {
    canvas = await html2canvas(inner, {
      scale: 1, useCORS: true, allowTaint: true,
      backgroundColor: null, logging: false,
      width: 1200, height: realH,
      windowWidth: 1200, windowHeight: realH
    });
  } catch(e) { console.error('renderMod error:', e); }

  document.body.removeChild(iframe);
  if (actions) actions.style.visibility = '';
  return canvas;
}

// 等待元素高度稳定（连续3次相同才返回）
async function waitForStableHeight(el, timeout = 1500) {
  return new Promise(resolve => {
    let lastH = 0, stableCount = 0;
    const start = Date.now();
    const check = () => {
      const h = el.scrollHeight;
      if (h > 0 && h === lastH) {
        stableCount++;
        if (stableCount >= 3) { resolve(h); return; }
      } else {
        stableCount = 0;
        lastH = h;
      }
      if (Date.now() - start > timeout) { resolve(h); return; }
      setTimeout(check, 80);
    };
    setTimeout(check, 100);
  });
}
```

### compressCanvas — 压缩到 2MB 以内

```js
function compressCanvas(canvas, maxBytes) {
  const png = canvas.toDataURL('image/png');
  if (png.length * 0.75 <= maxBytes) return { url: png, ext: 'png' };
  for (const q of [0.97, 0.94, 0.90, 0.85, 0.80, 0.72]) {
    const jpg = canvas.toDataURL('image/jpeg', q);
    if (jpg.length * 0.75 <= maxBytes) return { url: jpg, ext: 'jpg' };
  }
  return { url: canvas.toDataURL('image/jpeg', 0.72), ext: 'jpg' };
}
```

### expMod — 单模块导出

```js
async function expMod(id) {
  const label = document.getElementById(id).querySelector('.mod-label').textContent;
  toast('⏳ 渲染中...');
  const canvas = await renderMod(id);
  if (!canvas) { toast('渲染失败'); return; }
  const r = compressCanvas(canvas, 2 * 1024 * 1024);
  const a = document.createElement('a');
  a.download = safeFileName(BRAND.name) + '_' + safeFileName(label) + '_1200px.' + r.ext;
  a.href = r.url;
  a.click();
  toast('✓ 已导出 ' + canvas.width + '×' + canvas.height + 'px');
}
```

### expZip — ZIP 打包（逐个渲染，立即释放 canvas）

```js
async function expZip() {
  const mods = [...document.querySelectorAll('.mod-wrapper')];
  if (!mods.length) { toast('还没有模块'); return; }
  toast('⏳ 打包中...', 15000);
  const zip = new JSZip();
  for (let i = 0; i < mods.length; i++) {
    const label = mods[i].querySelector('.mod-label').textContent;
    const idx = String(i + 1).padStart(2, '0');
    const canvas = await renderMod(mods[i].id);
    if (!canvas) continue;
    const r = compressCanvas(canvas, 2 * 1024 * 1024);
    // 渲染完立刻转 dataURL，canvas 对象释放，避免内存溢出
    zip.file(idx + '_' + safeFileName(BRAND.name) + '_' + safeFileName(label) + '.' + r.ext,
      r.url.split(',')[1], { base64: true });
    await new Promise(res => setTimeout(res, 200));
  }
  const blob = await zip.generateAsync({ type: 'blob' });
  const a = document.createElement('a');
  a.download = safeFileName(BRAND.name) + '_店铺模块.zip';
  a.href = URL.createObjectURL(blob);
  a.click();
  toast('✓ ZIP 下载完成，共 ' + mods.length + ' 个模块');
}
```

### expLong — 合并长图（用 Image 对象合并，不堆积 canvas）

```js
async function expLong() {
  const mods = [...document.querySelectorAll('.mod-wrapper')];
  if (!mods.length) { toast('还没有模块'); return; }
  toast('⏳ 合并长图中...', 30000);

  // 逐个渲染，转 dataURL 后释放 canvas
  const frames = [];
  for (const mod of mods) {
    const canvas = await renderMod(mod.id);
    if (!canvas) continue;
    frames.push({ url: canvas.toDataURL('image/jpeg', 0.92), w: canvas.width, h: canvas.height });
    await new Promise(r => setTimeout(r, 200));
  }

  // 用 Image 对象绘制到 merged canvas，不持有多个 canvas
  const totalH = frames.reduce((s, f) => s + f.h, 0);
  const merged = document.createElement('canvas');
  merged.width = 1200; merged.height = totalH;
  const ctx = merged.getContext('2d');
  let y = 0;
  for (const f of frames) {
    await new Promise(resolve => {
      const img = new Image();
      img.onload = () => { ctx.drawImage(img, 0, y); y += f.h; resolve(); };
      img.src = f.url;
    });
  }

  const r = compressCanvas(merged, 10 * 1024 * 1024); // 长图放宽到 10MB
  const a = document.createElement('a');
  a.download = safeFileName(BRAND.name) + '_首页长图.' + r.ext;
  a.href = r.url;
  a.click();
  toast('✓ 长图已导出 1200×' + totalH + 'px');
}
```

### safeFileName — 文件名安全处理

```js
function safeFileName(str) {
  return (str || 'module').replace(/[^\w\u4e00-\u9fa5\-]/g, '_').slice(0, 40);
}
```

### 导出三件套必须引入的库

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
```

---

## 字体规范

字体是品牌调性的核心，**不能写死**。在品牌配置对象里定义，根据风格关键词选择合适的字体组合。

### 字体预设（根据品牌风格选择）

| 风格 | 中文字体 | 英文字体 | Google Fonts 参数 |
|---|---|---|---|
| 高级感 / 极简 / 珠宝 | Noto Serif SC | Cormorant Garamond italic | `Noto+Serif+SC:wght@200;300;400&Cormorant+Garamond:ital,wght@0,300;1,300` |
| 活泼 / 甜美 / 国潮 | ZCOOL KuaiLe | DM Sans | `ZCOOL+KuaiLe&DM+Sans:wght@300;400` |
| 工装 / 户外 / 运动 | Noto Sans SC | Space Grotesk | `Noto+Sans+SC:wght@300;400;500&Space+Grotesk:wght@300;400;500` |
| 复古 / 中式 / 文化 | ZCOOL XiaoWei | Playfair Display | `ZCOOL+XiaoWei&Playfair+Display:ital,wght@0,400;1,400` |
| 现代 / 科技 / 简约 | Noto Sans SC | Inter | `Noto+Sans+SC:wght@300;400&Inter:wght@300;400` |
| 手工艺 / 温暖 / 生活 | Ma Shan Zheng | Lora | `Ma+Shan+Zheng&Lora:ital,wght@0,400;1,400` |

### 品牌配置里的字体定义

在生成 HTML 时，字体通过 `BRAND` 对象统一管理，CSS 变量派生自它：

```js
const BRAND = {
  name: '品牌名',
  nameEn: 'BRAND',
  // ... 颜色 ...

  // 字体：根据风格选预设，或用户指定
  fontCN: '"Noto Serif SC", serif',       // 中文主字体
  fontEN: '"Cormorant Garamond", serif',   // 英文装饰字体
  fontENStyle: 'italic',                   // 英文是否斜体
  googleFontsUrl: 'https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@200;300;400;500&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&display=swap',
};
```

对应的 CSS 变量：
```css
:root {
  --font-cn: var(--brand-font-cn, "Noto Serif SC", serif);
  --font-en: var(--brand-font-en, "Cormorant Garamond", serif);
}
```

iframe 导出时，`<link>` 的 href 从 `BRAND.googleFontsUrl` 读取，不硬编码：
```js
iDoc.write(`...
  <link href="${BRAND.googleFontsUrl}" rel="stylesheet">
...`);
```

### 字号（1200px 画布，与字体无关）

- 品牌名大标题：80–100px，weight 300
- 系列名：52–68px，weight 300
- 段落正文：18–20px，weight 300，line-height 2.2–2.5
- 小标签/编号：11–14px，letter-spacing 4–6px