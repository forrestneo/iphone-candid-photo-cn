# 结构化提示词 Schema(中文输出)

仅当用户要求 JSON、提示词审计、自动化输出或严格源测试时阅读本文件。

返回单个合法 JSON 对象。不要使用注释、Markdown 围栏、尾随逗号,对象外不要有任何文字。

```json
{
  "meta_data": {
    "style": "iPhone Pro Max Photography",
    "aspect_ratio": "9:16"
  },
  "prompt_components": {
    "subject": "人物细节、穿搭、姿势与人物关系(简体中文)",
    "environment": "背景、地点与社交情境(简体中文)",
    "lighting": "Smart HDR 式光比表现,自然光或直接闪光光源(简体中文)",
    "camera_gear": "iPhone 16 Pro Max, 主摄 24mm f/1.78",
    "processing": "Apple ProRAW, Deep Fusion, Shot on iPhone",
    "imperfections": "贴合情境的数码噪点、运动模糊、皮肤纹理、曝光失误或构图瑕疵(简体中文)"
  },
  "full_prompt_string": "把以上字段合并成的一段自包含的、逗号分隔的中文提示词",
  "negative_prompt": "专业相机, 单反, 焦外光斑, 变形宽银幕, 电影灯光, 影棚灯光"
}
```

## 字段规则

- `subject` 忠实于用户请求与参考图,不得悄悄改写身份、年龄、体型、族裔或关系。
- `environment` 用来补全模糊的地点,不要发明新剧情。
- `camera_gear` 只写一个镜头,不要列出备选。产品名与镜头参数保留原文格式,例如 "iPhone 16 Pro Max, 前置摄像头 13mm f/2.2"。
- `processing` 保持为审美目标,不要声称生成的文件是真正的 Apple ProRAW 或真实相机拍摄。
- 只选相关的瑕疵。人物优先选毛孔、绒毛、轻微色调不均和局部高光,而非均匀油光。
- `full_prompt_string` 必须自包含,下游图像模型不需要读其他字段。除专有名词外全部用简体中文书写。
- 用户要求的排除项加入 `negative_prompt`;严格源测试模式下,只保留上面六个默认排除项。

## 参考图记法

当 JSON 需要描述参考图时,在现有字段内部标明角色,不要改动 schema。例:`"subject": "人物身份与参考图 1 一致,姿势与参考图 2 一致……"`
