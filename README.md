# -skills
将任意格式文章排版为html文档
<div align="center">

# ✨ WeChat Format

**一键把普通文章变成能直接发的公众号排版**

*Turn plain text into publish-ready WeChat articles. One command.*

[![Skill](https://img.shields.io/badge/Claude-Skill-8A63D2)](https://docs.claude.com/en/docs/claude-code/skills)
[![Version](https://img.shields.io/badge/version-1.0-blue)]()
[![License](https://img.shields.io/badge/license-MIT-green)]()
[![Lang](https://img.shields.io/badge/docs-中文%20%7C%20EN-orange)]()

[中文文档](#中文) · [English](#english)

</div>

---

<div align="center">

```
  粘贴文章  ──→  识别类型  ──→  套用配色  ──→  输出 HTML
  paste         detect          theme          ready to paste
```

</div>

---

<a name="中文"></a>

## 中文

排版是写作里最不值得花时间的一环。你写完了三千字，然后花四十分钟调字号、对齐引用框、给小标题挑颜色 —— 这件事完全可以交出去。

这个 skill 做的就是这件事：读懂你的文章结构，判断它属于哪一类，然后套上一整套已经调好的排版方案，直接产出可以粘进公众号编辑器的 HTML。

### 它解决什么

| 痛点 | 这里怎么处理 |
|------|-------------|
| 字号大小全靠感觉 | 一套速查表定死：大标题 22-24px、小标题 18-19px、正文 15-16px、辅助信息 14px |
| 纯黑字太刺眼 | 正文统一 `#3F3F3F` 深灰，标题 `#1A1A1A`，全部经过对比度校准 |
| 每篇都要重挑颜色 | 五种文章类型各有主色，识别后自动套用 |
| 引用框、提示框懒得写 | 内置组件库，直接调用 |
| 手机上看着挤 | 行高 1.6-1.8、段间距 20-25px、677px 容器宽度 |
| 外部 CSS 被微信吃掉 | 全部内联样式，粘过去不掉格式 |

### 五种风格

不是换个色号那么简单，每一类的组件形态都不一样。

| 类型 | 主色 | 视觉特征 |
|------|------|---------|
| 🔬 **科技/技术** | 蓝 `#3498DB` | 冷色调、深色代码块、术语高亮、左侧色块小标题 |
| 🔥 **观点/评论** | 红橙 `#E74C3C` | 核心观点走引用框、渐变高亮块、关键句标色 |
| 🌿 **生活/情感** | 暖黄 `#F5B041` | 大间距、装饰分隔线 `✦ ✦ ✦`、柔和居中小标题 |
| 📚 **教育/教程** | 蓝绿 `#27AE60` | 胶囊步骤标记、⚠️ 注意框、💡 提示框 |
| 📰 **资讯/新闻** | 灰蓝 `#2C3E50` | 信息卡片、数据放大标红、时间线 |

风格可以自动判断，也可以直接指定：

```
/科技   /观点   /生活   /教程   /资讯   /简洁   /鲜艳
```

### 三种输入

```
① 直接粘贴正文
② 丢一个链接         → 自动抓取
③ 给一个文件路径     → 自动读取
```

Markdown 和纯文本都能处理。没有任何标记的大段文字也认得出来 —— 独立成行的短句当小标题，「一、」「1.」「第一章」这类序号识别为章节，引号包裹的独立行判为引用，`{ } ; =` 密集出现的连续行判为代码。

### 用起来

放进 skill 目录：

```bash
# Claude Code
~/.claude/skills/wechat-format/SKILL.md

# 项目级
.claude/skills/wechat-format/SKILL.md
```

然后正常说话就行：

```
帮我排版这篇文章：<粘贴内容>

用生活类风格排一下 https://example.com/article

/教程 ~/Documents/tutorial.md
```

拿到的东西：HTML 文件路径、结构分析（识别出几个小标题、几处引用）、排版说明、视觉效果描述。

### 输出到哪

按优先级取第一个可用的，不写死任何绝对路径：

1. 你在对话里直接说 —— 「存到 `~/Documents/公众号/`」
2. 环境变量 `WECHAT_FORMAT_OUTPUT_DIR` —— 配一次长期生效
3. 当前目录下的 `./公众号文章/` —— 兜底，跨平台

```bash
# 想固定下来就加到 shell 配置里
export WECHAT_FORMAT_OUTPUT_DIR="$HOME/Documents/公众号文章"
```

目录不存在会自动建，重名文件追加 `-2`、`-3`，不覆盖已有内容。

### 发布流程

1. 让 skill 排好版，拿到 HTML
2. 浏览器打开，全选复制
3. 粘进公众号编辑器
4. 图片单独上传（微信不吃外链图片）

### 组件清单

头部（简洁/渐变）· 首字下沉段落 · 三种小标题 · 三种引用 · 四种重点标注 · 三种列表 · 四种分隔线 · 图片带说明 · 总结框 · 拓展阅读框 · 互动框 · 三种结尾（含二维码位、作者卡片）

### 想改

配色、字号、组件样式全在 SKILL.md 里，纯文本，直接改。加自己的品牌色，或者往「通用排版组件库」那节里塞新组件都可以。

---

<a name="english"></a>

## English

Formatting is the least valuable part of writing. You finish three thousand words, then spend forty minutes nudging font sizes, aligning quote blocks, and picking a color for your section headings. That work can be handed off.

This skill reads your article's structure, figures out what kind of piece it is, applies a pre-tuned typographic system, and hands back HTML you can paste straight into the WeChat editor.

### What it fixes

| Problem | How it's handled |
|---------|-----------------|
| Font sizes chosen by vibe | A fixed scale: 22-24px titles, 18-19px headings, 15-16px body, 14px captions |
| Pure black is harsh on screens | Body locked to `#3F3F3F`, titles `#1A1A1A`, all contrast-checked |
| Re-picking colors every article | Five article types, each with its own palette, applied automatically |
| Hand-writing callout boxes | Built-in component library |
| Cramped on mobile | 1.6-1.8 line height, 20-25px paragraph gaps, 677px container |
| WeChat strips external CSS | Everything inlined, nothing breaks on paste |

### Five styles

Not just a hue swap — the component shapes differ per type.

| Type | Accent | Visual signature |
|------|--------|-----------------|
| 🔬 **Tech** | Blue `#3498DB` | Cool tones, dark code blocks, highlighted jargon, left-bar headings |
| 🔥 **Opinion** | Red-orange `#E74C3C` | Thesis in quote blocks, gradient highlights, colored key sentences |
| 🌿 **Lifestyle** | Warm gold `#F5B041` | Generous spacing, `✦ ✦ ✦` dividers, soft centered headings |
| 📚 **Tutorial** | Blue-green `#27AE60` | Pill step markers, ⚠️ warning boxes, 💡 tip boxes |
| 📰 **News** | Slate `#2C3E50` | Info cards, enlarged red stats, timelines |

Detected automatically, or force one:

```
/科技 (tech)  /观点 (opinion)  /生活 (life)
/教程 (tutorial)  /资讯 (news)  /简洁 (minimal)  /鲜艳 (vivid)
```

### Three inputs

```
① Paste the text
② Drop a URL          → fetched automatically
③ Give a file path    → read automatically
```

Markdown and plain text both work. Even wholly unmarked prose gets parsed: short standalone lines become headings, numbered prefixes like `一、` / `1.` / `第一章` become sections, quoted standalone lines become pull quotes, and consecutive lines dense with `{ } ; =` become code blocks.

### Install

```bash
# Claude Code, personal
~/.claude/skills/wechat-format/SKILL.md

# Project-scoped
.claude/skills/wechat-format/SKILL.md
```

Then just ask:

```
Format this article for WeChat: <paste>

Format https://example.com/article in lifestyle style

/教程 ~/Documents/tutorial.md
```

You get back: the HTML file path, a structure breakdown (headings found, quotes found), notes on what was applied, and a description of the visual result.

### Where output goes

First available wins — no absolute path is hardcoded:

1. Whatever you say in the conversation — "save it to `~/Documents/wechat/`"
2. `WECHAT_FORMAT_OUTPUT_DIR` — set once, applies from then on
3. `./公众号文章/` under the current directory — cross-platform fallback

```bash
# Make it permanent in your shell config
export WECHAT_FORMAT_OUTPUT_DIR="$HOME/Documents/wechat-articles"
```

Missing directories are created. Name collisions get `-2`, `-3` suffixes rather than overwriting anything.

### Publishing

1. Run the skill, get the HTML
2. Open it in a browser, select all, copy
3. Paste into the WeChat editor
4. Upload images separately — WeChat rejects hotlinked images

### Components

Headers (plain/gradient) · drop-cap paragraphs · 3 heading styles · 3 quote styles · 4 emphasis styles · 3 list styles · 4 dividers · captioned images · summary boxes · further-reading boxes · discussion prompts · 3 endings (QR slot, author card)

### Customizing

Colors, sizes, and component markup all live in SKILL.md as plain text. Edit it. Swap in your brand palette, or add components under the 通用排版组件库 section.

---

<div align="center">

**MIT** · PRs and new style presets welcome

*写作归你，排版归它。*
*You write. It formats.*

</div>

