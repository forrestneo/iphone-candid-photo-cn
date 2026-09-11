# iPhone 随手拍 · 中文提示词 Skill

把一句简短的场景描述,变成可信的「iPhone 随手拍」风格照片提示词 —— **全中文输出**,适配即梦、豆包、可灵等对中文提示词服从度更好的生图工具。

> Turn short scene descriptions into believable iPhone-style candid photo prompts — with Simplified Chinese output. A Chinese-output fork of [aijiduonadegou/iphone-photo](https://github.com/aijiduonadegou/iphone-photo) (MIT).

## 它解决什么问题

- **中文提示词输出**:所有提示词字段默认简体中文,产品名与镜头参数(`iPhone 16 Pro Max`、`24mm f/1.78`)保留原文作为风格锚点;
- **手机镜头语言**:24mm 主摄(默认抓拍)/ 13mm 超广角(臂距自拍、狭窄空间)/ 77mm 长焦(远距离不打扰),按场景有意识地选一个;
- **克制的瑕疵感**:只选 2~4 个贴合情境的缺陷(数码噪点、轻微手抖、构图歪斜、真实皮肤微纹理),明确禁止均匀油光与磨皮 —— 避免"一眼 AI";
- **参考图保真**:身份参考、姿势参考、编辑目标分角色管理,不得擅自美化、改龄、换身份;
- **结构化输出**:标准 JSON 提示词契约 + 可审计的严格源测试模式。

## 安装

复制整个文件夹到 ZCode 的用户级 skills 目录:

```text
~/.zcode/skills/iphone-candid-photo-cn/
```

Windows 默认:

```text
C:\Users\<你>\.zcode\skills\iphone-candid-photo-cn\
```

采用标准 `SKILL.md` 格式,同样兼容 Codex(复制到 `$CODEX_HOME/skills/` 即可)。**复制后新开一个会话**才会被发现。

## 用法

直接生成(有图像工具时默认直接出图):

```text
用 iPhone 随手拍风格生成:雨夜便利店门口的朋友合影。
```

只要中文 JSON 提示词(不生成图):

```text
只输出中文 JSON 提示词,不要生成图片:车内自拍,驾驶位,金色大圈耳环……
```

英文回退:

```text
输出英文版提示词:黄昏天台上的闺蜜合影。
```

## 输出示例

场景:「车内自拍,成熟上海女性,驾驶位,金色大圈耳环」→

```json
{
  "meta_data": {
    "style": "iPhone Pro Max Photography",
    "aspect_ratio": "9:16"
  },
  "prompt_components": {
    "subject": "一位成熟美丽的上海女性坐在汽车驾驶位自拍,一只手臂前伸拿着手机,另一只手轻托下巴……",
    "camera_gear": "iPhone 16 Pro Max, 前置摄像头 13mm f/2.2",
    "imperfections": "细腻的数码传感器噪点,真实皮肤微纹理……轻微手持抖动"
  },
  "full_prompt_string": "生活化前置摄像头 iPhone 自拍,一位成熟美丽的上海女性坐在汽车驾驶位……浅景深,iPhone 16 Pro Max 前置摄像头 13mm f/2.2,Apple ProRAW 色彩,Deep Fusion 局部细节,Shot on iPhone,氛围感,高清日常纪实快照",
  "negative_prompt": "专业相机, 单反, 焦外光斑, 变形宽银幕, 电影灯光, 影棚灯光"
}
```

完整契约见 [references/schema.md](references/schema.md)。

## 与原版的差异

| | 原版 iphone-photo | 本版 iphone-candid-photo-cn |
|---|---|---|
| 提示词输出语言 | 英文 | **简体中文**(专有名词保留原文) |
| 负面提示词 | 英文六项默认 | 中文对应项 |
| 英文回退 | — | 用户明确要求时输出英文 |
| 工作流(模式/镜头/瑕疵/自检) | ✓ | 保持一致(正文已中文化) |

## 文件结构

```text
iphone-candid-photo-cn/
├── SKILL.md            # 核心行为与生成工作流(中文)
├── references/
│   └── schema.md       # JSON 提示词契约(中文输出版)
├── agents/
│   └── openai.yaml     # 客户端界面元数据
├── NOTICE.md           # 来源与署名
└── LICENSE             # MIT
```

## 署名与许可

本 skill 是 [aijiduonadegou/iphone-photo](https://github.com/aijiduonadegou/iphone-photo)(MIT)的中文输出改造版;原版灵感来自 Machina(`@EXM7777`)公开分享的移动摄影元提示,详见 [NOTICE.md](NOTICE.md)。

许可为 MIT,覆盖本独立改写的实现;不授予第三方商标、参考图、角色或其他用户素材的权利。
