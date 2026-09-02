---
title: "涂鸦影子合照 - 角色参考图转写提示词"
date: 2026-09-02
category: ai/prompts/image-generation
tags: [image-generation, prompt, portrait, character-reference, doodle, shadow, mixed-media]
source: custom
author: 云归
related: [engineering-blueprint-style]
---

# 涂鸦影子合照 - 角色参考图转写提示词

> **来源**: 云归自定义
> **类型**: 图像生成提示词 (Image Generation Prompt)
> **适用模型**: 支持角色参考图 (character reference) + 图像生成的模型
> **整理时间**: 2026-09-02

---

## 提示词原文 (Prompt)

```
Use the uploaded character reference image as the strict identity and outfit reference. Preserve the reference character's:\n- face identity\n- facial proportions\n- eye shape\n- nose\n- lips\n- skin tone\n- hairstyle\n- hair color\n- visible hair accessories\n- overall recognizable vibe
- outfit and styling shown in the reference image
Do not hardcode any specific character traits that are not present in the uploaded reference. All identity, hairstyle, accessories, and clothing details must be inferred directly from the uploaded reference image.

Create a high-quality mixed-style vertical portrait showing:
1. a realistic full-body version of the uploaded character/person
2. a black hand-drawn doodle-shadow version of the same character/person on the wall beside them

Core concept:
The real person and their doodle-shadow are doing a playful mischievous pose together. The real person performs a cute realistic version of the pose, while the doodle-shadow performs a much more exaggerated, chaotic, cartoonish version of the same pose idea. The mood should feel cute, playful, mischievous, stylish, funny, and social-media-friendly.

Real person:
- Must remain realistic and photogenic
- Must wear the same outfit style and key visible details from the uploaded reference image
- Do not replace the reference styling with unrelated fashion
- Expression should be cute, slightly confused, mildly embarrassed, playful, as if thinking: "Why am I doing this with my shadow?"
- The real person should not stand stiffly
- The real person should actively participate in the pose, but in a natural realistic way

Doodle-shadow:
- Must be a black hand-drawn sketch version of the same person, drawn directly on the wall
- Not a realistic second person
- Not a normal physical shadow
- Not a full-color anime character
- Black sketch line-art only
- Should resemble the person through hairstyle silhouette, accessories, outfit silhouette, and pose structure
- The doodle-shadow should look more energetic, sillier, and more chaotic than the real person
- Add manga-like motion lines, hearts, stars, sparkles, and comic marks around the doodle if helpful

Random mischievous pose rule:
The pose must NOT be fixed. For each generation, invent a new playful mischievous pose for both the real person and the doodle-shadow. The real person and the doodle-shadow should share the same general pose idea, but they do not need to match perfectly. The real person performs a cute realistic version. The doodle-shadow performs a much more exaggerated, chaotic, cartoonish version.
Do not repeatedly use pointing poses.
Do not repeatedly use finger-gun poses.
Do not repeatedly use the same standing pose.
Do not always make both figures simply point at each other.
Create a different mischievous pose each time.

Possible pose directions are loose inspiration only, not a fixed menu:
- playful idol pose
- silly dance pose
- leaning sideways with one arm curved overhead
- making a big heart pose
- cheeky wink pose
- hands near cheeks in a cute teasing pose
- exaggerated "ta-da!" pose
- mock surprise pose
- playful running-in-place pose
- mischievous tiptoe pose
- arms stretched in opposite directions
- pretending to sneak away
- cute troublemaker pose
- dramatic overreaction pose
- goofy victory pose
- playful balance pose
- playful peekaboo pose
- shy but mischievous pose
- cute overconfident pose

The final pose should feel fresh, cute, mischievous, and slightly chaotic. The real person should look like they are reluctantly playing along. The doodle-shadow should look like it is having way too much fun.

Composition:
- vertical 4:5 or 9:16
- show the real person in full-body or nearly full-body framing
- place the real person on one side of the frame
- place the black doodle-shadow on a clean wall beside them
- the doodle-shadow should be roughly the same height or slightly taller
- keep enough space around both figures so the full pose is visible
- the connection between the real person and the doodle-shadow must be clear at a glance

Background:
- simple clean indoor studio wall or minimal room corner
- white, cream, or pale gray wall
- clean floor
- soft natural sunlight patch or gentle wall shadow allowed
- keep the background uncluttered

Lighting:
- soft natural studio lighting
- bright, clean, polished, playful mood
- keep the real person's face clearly visible

Style quality:
- realistic human photography
- black hand-drawn doodle-shadow on wall
- matching mischievous pose interaction
- strong identity resemblance
- outfit and styling faithfully based on the uploaded reference
- cute and stylish mixed-media portrait
- clean composition
- social-media-friendly
- no obvious AI artifacts

Negative prompt:
hardcoded blue hair when not in reference, hardcoded cloud clip when not in reference, hardcoded fish clip when not in reference, hardcoded school uniform when not in reference, outfit change unrelated to reference, realistic second person, normal reflection, normal shadow only, solid black monster shadow, horror shadow, creepy shadow, full-color illustration, cartoon human, anime human, weak resemblance, unrelated sketch character, messy wall, cluttered background, repeated pointing pose, repeated finger-gun pose, same pose every time, fixed pose, boring mirrored pose, stiff pose, identical pose repetition, real person not matching shadow pose, text, watermark, logo, distorted body, extra limbs, extra fingers, bad hands

Score repair (the only appended change; preserve every source camera/action/composition/foreground/light/scene invariant):
Keep the successful real-person/doodle relationship but rotate to a different clearly adult Gallery appearance and a fresh mischievous pose, with this family limited to low frequency rather than appearing in every batch.
```

---

## 使用说明

1. **必须上传角色参考图**: 此提示词依赖上传的角色/人物参考图，所有身份特征（脸型、发型、配饰、服装）都从参考图推断
2. **禁止硬编码特征**: 不要预设参考图中没有的特征（如蓝发、云朵发夹、鱼形发夹、校服等），这些只出现在负面提示词中作为"非参考时禁用"
3. **每次生成换新姿势**: 提示词明确要求每次生成随机发明新的恶作剧姿势，避免重复
4. **适用场景**: 社交媒体头像、趣味角色二创、真人+涂鸦混合风格照片
