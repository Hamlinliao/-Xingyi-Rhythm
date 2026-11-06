# 兴义点线 · Xingyi Rhythm

> 把任意一张图片，拆成点、线、面，再重新编排成一张吴冠中式的程序化山水。
<img width="565" height="419" alt="image" src="https://github.com/user-attachments/assets/234624d7-415d-4e32-8042-395da18e82bf" />


![Text License](https://img.shields.io/badge/text-MIT-1F2422)
![Asset License](https://img.shields.io/badge/stills-CC%20BY--NC%204.0-B34532)
![Format](https://img.shields.io/badge/format-Agent%20Skill-2F7068)
![Input](https://img.shields.io/badge/input-any%20image-D6B24C)

**兴义点线**是一个可安装的视觉 Skill：给它一张照片、插画、宠物、人物、产品或建筑图，它会先留白，再用墨线、灰面、色点与几何模块重新编排；也可以继续把这张图变成 5–8 秒的“线条生长 / 色点散开 / 村落拼装 / 回到白纸”的图生视频。

它提炼自《贵州兴义》约 40.4 秒的影像，但**不要求输入图里有山、有村、有向日葵**。可迁移的是点线面的构成方法，不是原片的地标。

---

## 它做什么

- **任意图片二创**：人像、宠物、产品、建筑、风景、街拍、角色。
- **点线面重构**：不是水墨滤镜，而是先拆成模块，再按预算重组。
- **程序化 score**：把一张图分解成 12×8 网格、色板、点/线/面预算、主路径与锚点，输出 JSON + 网格预览。
- **图生视频**：线生长、面铺开、点散开、屋顶拼装、雾擦除；一条镜头只做一个动作。
- **提示词包**：8 份中英双语 `.txt`，适配 Midjourney / SD / ComfyUI / 即梦 / 可灵 / 通义万相。
- **验收标准**：留白、黑白灰、线质量、点节奏、主体保真、纸感与套色错位。

## 它不做什么

- 不训练模型、不包含权重、不是 LoRA。
- 不复制吴冠中的任何具体作品；它是风格方法论的研究与转译。
- 不保证“一键出片”；它给的是构图规则、score 与提示词。
- 不把参考帧或 score 说成生成结果。
- 不适用于写实摄影、3D 渲染、赛博霓虹、日式赛璐璐；也不用于《下山》的靛蓝重彩（用 `indigo-descent`）。

---

## 30 秒上手

把下面这段和图片一起发给 agent：

```text
用 xingyi-rhythm 把这张图转成吴冠中式点线面山水。
保留：[脸型/发型/眼镜；或宠物毛色/耳形；或产品外形/logo 位置]。
L2 半抽象：拆成 2–4 块面、4–8 条线、2–4 簇点；留白 55%；
一条主路径，3–7 组屋顶，色点 120，红只留 1 簇；不要文字，不要加马。
```

只想复制提示词？直接拿这两段：

```text
暖米白宣纸上的吴冠中式点线面山水。焦墨线为骨，提按、断连、飞白；灰、银灰、青灰、土黄平涂为面，边缘干笔；彩色点成簇，黄/红/绿/蓝不超过六种，红只做 1–3 簇；留白 40–65%，手工印刷般轻微套色错位，形式美与抽象美，但保留 1–2 个可读锚点。

主体：[...]，保留 [2–3 个识别点]。L2：拆成 [2–4] 块面、[4–8] 条线、[2–4] 簇点；主体偏 [左/右]；留白 [55]%；一条主路径；色点 [120]；红 [1] 簇。

负向：写实摄影，3D 渲染，等宽描边，矢量填色，满屏彩点，均匀噪点，彩虹渐变，随机文字，水印，多余肢体，脸崩。
```

---

## 预览

一张纸的生成过程：白纸起笔 → 山体生成 → 田园拼装 → 花与点题 → 村落落位 → 回到白纸。
<img width="560" height="390" alt="截屏2026-11-06 17 42 51" src="https://github.com/user-attachments/assets/587e2387-6c34-434b-9c1c-b70472e702c5" />


点、线、面三种模块，以及它们各自的预算与禁忌：

  <img width="564" height="709" alt="image" src="https://github.com/user-attachments/assets/447cd872-03bc-4a78-90cc-83a9a0a0ca80" />

色板与面积比例：

![Uploading image.png…]()


---

## 安装

### Claude Code

```bash
git clone <your-repo-url> ~/.claude/skills/xingyi-rhythm
```

把 `<your-repo-url>` 换成你的 GitHub 仓库地址。

项目内使用：

```bash
mkdir -p .claude/skills
cp -R xingyi-rhythm .claude/skills/
```

确保 `SKILL.md` 位于技能目录根部：

```text
.claude/skills/xingyi-rhythm/
├── SKILL.md
├── references/
├── prompts/
├── scripts/
└── assets/
```

### Codex / 其他 Agent

把整个目录放进 agent 的 skills 目录（常见为 `~/.codex/skills/`，以你的版本为准），或直接引用：

```text
请阅读 xingyi-rhythm/SKILL.md，并按 references/procedural-grammar.md 的 score 流程处理我上传的图片。
```

### ChatGPT / Custom GPT / Project

- 把 `SKILL.md` 贴进 Instructions。
- 把 `references/*.md` 与 `prompts/*.txt` 作为知识文件上传。
- 图片二创仍需外部图像生成工具；本 skill 负责读图、定 score、写提示词与验收。

### 只用提示词

不需要安装。直接打开：

- `prompts/style-lock.zh.txt` / `style-lock.en.txt`
- `prompts/image-transfer.zh.txt` / `image-transfer.en.txt`
- `prompts/video.zh.txt` / `video.en.txt`
- `prompts/negative.zh.txt` / `negative.en.txt`

---

## 用法

### 1. 任意图片二创

```text
用 xingyi-rhythm 处理这张照片：
保留我的圆脸、短发和圆框眼镜；L2 半抽象；脸用 3 条线 + 1 块面；
衣服拆成 2 块靛蓝/灰面；左侧留白 55%；背景一块淡青灰 + 3 簇土黄/草绿点；
不要加马、不要加印章、不要文字；4:5。
```

Agent 应先读图、写“绝不能丢的三件事”，再选 L1/L2/L3 与构图，然后给 score、提示词与参数；有图像工具才实际生成。

### 2. 图生视频

```text
用这张已经风格化的图做 5 秒图生视频：
只做一个动作——一条墨线从右下向左上延伸，经过的地方浮出 2 块青灰/土黄淡染；
镜头极缓慢前推 2/10；纸纹、留白、色板保持稳定；不要出现屋顶、人物或文字。
```

先有风格化首帧或 score 图，再做图生视频。不要拿原始照片直接跑视频。

### 3. 用脚本生成 score

```bash
pip install -r requirements.txt
python scripts/xingyi_score.py input.jpg \
  --out score.json \
  --preview score-preview.png \
  --grid 12x8 \
  --seed 20261106
```

输出：

- `score.json` — 色板、留白目标、点/线/面预算、主路径、锚点、12×8 模块网格、提示词提示。
- `score-preview.png` — 在原图上叠加网格、模块字母、主路径与锚点。

脚本只依赖 Pillow + numpy，不需要 OpenCV/GPU；只做**分解与预算**，不渲染最终画面。把 score 的预算和 `prompts/` 的风格锁一起交给图像模型。

### 4. 做一组同风格图

- 复用同一段风格锁、同一张纸纹、同一套色板。
- 只改抽象级别、构图、点预算三个变量之一。
- 同一系列固定 seed；视频固定首帧与尾帧。
- 一致性来自重复，不来自堆形容词。

---

## 程序化：模块 + 参数 + 种子

“程序化”不是随机撒点，而是：

1. **先留白**：40–65% 的纸白/雾，先划出 `VOID`。
2. **再走线**：一条主路径穿过画面，4–12 条主次线；提按、断连、飞白。
3. **再压面**：2–4 块灰/青灰/土黄大面，边缘干笔，不做体积。
4. **再落模块**：3–7 组屋顶、点阵窗、树冠、田块网格。
5. **最后撒点**：40–200 个色点，成 3–5 簇，4–6 种颜色，红 ≤ 3 簇。
6. **收束**：用雾/纸白擦回，保留 1–2 个锚点。

| 参数 | 默认 | 作用 |
| --- | --- | --- |
| `abstraction` | 0.55 | 抽象级别；0.25 更具体，0.85 更抽象 |
| `white_space` | 0.52 | 留白目标；40–65% |
| `dot_budget` | 120 | 色点数量；40–200 |
| `line_energy` | 0.55 | 线的提按/断连/速度 |
| `plane_count` | 3 | 大面数量；2–4 |
| `module_repeat` | 0.55 | 村落/窗格的秩序感 |
| `accent_ratio` | 0.08 | 彩色面积；5–12% |
| `seed` | 任意整数 | 同 seed + 同 score 可复现 |

三种抽象级别：

- **L1 具象**：主体 45–65%，细节保留 60–70%；适合人像、产品、客户项目。
- **L2 半抽象**：主体 35–50%，拆成 2–4 块面 + 4–8 条线 + 2–4 簇点；默认。
- **L3 抽象**：主体 20–35%，只留一个符号；适合海报、艺术系列。

完整模块表、score 结构与伪代码见 [点线面语法](references/procedural-grammar.md)。

---

## 风格 DNA

| 维度 | 规则 |
| --- | --- |
| 纸 | 暖米白/宣纸白，纤维、水渍、颜料颗粒；留白 40–65% |
| 墨 | 焦墨线为骨，提按、断连、飞白；不是等宽描边 |
| 面 | 2–4 块平涂/淡染，边缘干笔；不做写实光影与体积 |
| 点 | 成簇、有大小变化、4–6 色；红 ≤ 3 簇；彩色总面积 5–12% |
| 构成 | 不对称平衡；大留白对小块密集；长线对短点；冷灰对暖黄 |
| 锚点 | “风筝不断线”：无论多抽象，保留 1–2 个可读锚点 |
| 质感 | 纸纹、墨晕、轻微套色错位；不要渐变、光晕、塑料高光 |

完整规则见 [风格 DNA](references/style-dna.md)，图片流程见 [任意图片的转译](references/image-transfer.md)，视频见 [运动与生成](references/video-motion.md)。

---

## 和另外两个 skill 的区别

| Skill | 视觉 | 适合 |
| --- | --- | --- |
| `xingyi-rhythm`（本仓库） | 吴冠中式点线面、半抽象、程序化 score | 任意图片的风格化；海报、封面、文化视觉 |
| `ink-wash-journey` | 青绿+水墨+田园游历，偏具象 | 贵州兴义式风景短片、旅行叙事 |
| `indigo-descent` | 靛蓝+朱砂+纸本重彩+巨物微人 | 人像、宠物、产品、史诗感主视觉 |

《贵州兴义》的影像同时可以走向“具象水墨游历”和“抽象点线面”两个方向。本仓库做的是后者：**把同一片风景拆成形式，而不是再画一遍风景。**

---

## 目录

```text
xingyi-rhythm/
├── SKILL.md                     # 技能入口：何时用、三种级别、执行流程、输出约定
├── README.md
├── LICENSE                      # 文本/代码：MIT
├── LICENSE-ASSETS               # 预览静帧/封面/GIF：CC BY-NC 4.0
├── CITATION.cff
├── style.json                   # 机器可读的色板、参数、模式
├── requirements.txt             # Pillow + numpy（只给 score 脚本用）
├── agents/
│   └── openai.yaml
├── references/
│   ├── style-dna.md             # 纸墨色、点线面、构图、抽象级别、反风格
│   ├── procedural-grammar.md    # 模块表、参数、score 结构、伪代码
│   ├── image-transfer.md        # 任意图片转译：保真、拆模块、强度、后期
│   ├── video-motion.md          # 生成动作、镜头、转场、稳定性
│   ├── prompt-library.md        # 中英模板、平台写法、完整示例
│   └── quality-check.md         # 六项硬检查、评分表、交付话术
├── prompts/
│   ├── style-lock.zh.txt
│   ├── style-lock.en.txt
│   ├── image-transfer.zh.txt
│   ├── image-transfer.en.txt
│   ├── video.zh.txt
│   ├── video.en.txt
│   ├── negative.zh.txt
│   └── negative.en.txt
├── examples/
│   ├── landscape.md
│   ├── portrait.md
│   ├── pet.md
│   ├── product.md
│   └── score-example.json
├── scripts/
│   ├── xingyi_score.py          # 图片 → score JSON + 网格预览
│   └── README.md
└── assets/
    ├── README.md
    ├── cover.jpg
    ├── contact-sheet.jpg
    ├── grammar.jpg
    ├── score-demo.png
    ├── palette.png
    ├── motion-preview.gif
    ├── icon.png
    └── still-01.jpg … still-06.jpg
```

---

## 发布到 GitHub 时

- 仓库名建议：`xingyi-rhythm`
- Description：`A Wu Guanzhong-inspired procedural point-line-plane visual skill, distilled from the Guizhou Xingyi landscape film.`
- Topics：`agent-skill` `wu-guanzhong` `procedural-art` `point-line-plane` `chinese-aesthetic` `image-to-image` `image-to-video`
- Social preview 用 `assets/cover.jpg`。
- 仓库已控制在 5 MB 以内；不要上传原视频（约 170 MB）。
- 如果改过参数，记得同步 `style.json` 与 `references/procedural-grammar.md`。

---

## 来源、致敬与边界

- 原作影像：《贵州兴义》，廖慧敏（Hamlin），约 40.4 秒，5094×2160。
- 风格坐标：吴冠中公开作品中的点线面、形式美、抽象美与“风筝不断线”。本 skill 是风格方法论的研究与转译，**不是复制任何具体作品**，也不代表吴冠中基金会、家属或任何机构。
- 原视频未包含在此仓库；仅保留低分辨率静帧、封面与约 4 秒预览 GIF，用于评论、研究与风格说明。
- 静帧/封面/GIF 版权归原作者所有，按 CC BY-NC 4.0 提供；转载或商用请先获得授权。

---

## English

**Xingyi Rhythm** is a portable visual skill that turns any input image—portrait, pet, product, architecture, landscape or character—into a Wu Guanzhong-inspired procedural landscape of dots, lines and planes. It starts with paper white, runs one calligraphic path, lays two to four flat washes, assembles roof/window/field modules, and scatters limited color dots while keeping one or two readable anchors.

It includes a style DNA, a point-line-plane grammar with modules and budgets, an image-transfer workflow, image-to-video motion rules, bilingual prompt packs, four worked examples, a Python score generator and a quality checklist. It does not train a model or ship weights, and it does not reproduce any specific Wu Guanzhong painting.

**License:** text and code MIT; preview stills, cover and GIF CC BY-NC 4.0. The original film remains © Liao Huimin (Hamlin). This is an independent style study.
