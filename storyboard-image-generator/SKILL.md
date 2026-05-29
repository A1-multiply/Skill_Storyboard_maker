---
name: a1-storyboard-maker
description: Create sequential connected storyboard sheet images from a user's idea, script, article, treatment, text reference, image reference, or rough brief. Use when Codex should ask for references, storyboard style, sheet/page count, cuts per sheet, and aspect ratio, then generate visually consistent numbered storyboard pages where the story continues across sheets. Multiple sheets are never alternate versions; cut numbers must continue across pages.
---

# A1 Storyboard Maker

Use this skill to turn a user brief into a sequence of connected storyboard sheet images. Preserve continuity across every sheet and cut: characters, wardrobe, props, setting, camera language, aspect ratio, mood, and visual style.

## Absolute Rule: Multiple Sheets Are One Continuing Story

When the user asks for multiple storyboard sheets/pages, they mean one storyboard sequence split across multiple pages.

- Never treat multiple sheets as different versions, options, drafts, or variations.
- Never generate the same sheet number twice unless the user explicitly asks for variants.
- Generate sheet 1, then sheet 2, then sheet 3, in order.
- Each later sheet must continue directly from the final cut of the previous sheet.
- Cut numbers must continue across sheets.
- If sheet 1 has cuts 01-06, sheet 2 must have cuts 07-12.
- If sheet 1 has cuts 01-08, sheet 2 must have cuts 09-16.
- If the user says "2장만 만들어", that means two sequential storyboard pages, not two alternate images.

## Terminology

- A sheet/page is one complete storyboard page image.
- A cut is one storyboard panel inside a sheet.
- If the user asks for 3 sheets/pages, create 3 separate sequential storyboard sheet images.
- Do not combine all sheets into one image.
- Do not interpret multiple sheets as multiple single-scene images unless the user explicitly asks for one cut per image.

## Intake

If the user has not provided enough detail, ask briefly for:

1. Reference material: text, script, article, image, storyboard sample, character description, or visual style reference.
2. Storyboard style: cinematic, webtoon, commercial pitch, rough pencil, animation board, product ad, documentary, etc.
3. Number of storyboard sheets/pages.
4. Cuts per sheet, if they care. If omitted, infer 6 or 8 cuts based on story density.
5. Aspect ratio. Default to 16:9.

When the user has no reference, offer two choices in Korean if the user is writing in Korean:

```markdown
원하는 스토리보드 스타일이나 참고 텍스트/이미지가 있으면 보내주세요.

1. 참고자료가 있어요
2. 참고자료 없이 초안부터 잡아주세요

몇 장으로 만들지, 한 장에 몇 컷을 넣을지, 원하는 비율이 있으면 같이 알려주세요. 비율이 없으면 기본 16:9로 만들게요.
```

If the user chooses option 1, ask them to provide the reference if they have not already done so.

If the user chooses option 2, accept a short draft idea such as "SF ad", "cafe romance", "startup intro video", or "horror mood" and expand it into a coherent storyboard.

## Planning Workflow

Before generating images, create a compact continuity plan:

1. Story premise in one sentence.
2. Visual style: medium, mood, palette, detail level, and lighting.
3. Continuity bible: recurring characters, wardrobe, props, setting, time of day, and reference constraints.
4. Sheet list: exactly the requested number of sheets, numbered from 1 to N.
5. Cut list: cuts inside each sheet, with numbering that must continue across sheets.
6. Aspect ratio: user requested ratio, otherwise 16:9.
7. Generation order: sheet 1 first, sheet 2 next, never restarting at sheet 1.

Use this format for a 2-sheet, 6-cuts-per-sheet storyboard:

```markdown
1장 [이 페이지에서 진행되는 이야기]
- 01컷 [시작 장면]
- 02컷 [01컷에서 이어지는 행동]
- 03컷 [상황 확장]
- 04컷 [중요한 전환]
- 05컷 [갈등 또는 발견]
- 06컷 [2장으로 넘어가는 연결점]

2장 [1장에서 이어지는 이야기]
- 07컷 [06컷 직후 이어지는 행동]
- 08컷 [상황이 확장되는 장면]
- 09컷 [핵심 선택 또는 위기]
- 10컷 [해결 방향]
- 11컷 [결과 또는 공개]
- 12컷 [마무리 또는 다음 시퀀스 연결점]
```

Plan all requested sheets before creating the first image. The sheets must be one continuous sequence, not disconnected concepts and not alternate versions.

## Default Sheet Layout

When no layout reference is provided, make each sheet look like a clean production storyboard page:

- Header: `STORYBOARD | [project or story title]`.
- Optional concept line on the right.
- Numbered cut cards in a readable grid.
- Each cut card includes an image area, cut number, short title, shot type, and compact rows for ACTION, DIALOGUE, and TEXT.
- Optional notes box for tone, color, music, narration, runtime, or production notes.

Use Korean labels when the user writes in Korean. Keep on-image text short and legible. Also provide exact cut descriptions in the chat response because image models may distort small text.

## Image Generation Rules

Use the available image generation capability for raster image output.

- Generate one separate image per storyboard sheet.
- Use unique sheet numbers in prompts: sheet 1 of N, sheet 2 of N, sheet 3 of N.
- Continue cut numbers across sheets. Do not restart at 01 after sheet 1.
- For sheet 2 and later, include the previous sheet's final cut as the starting state.
- Keep the same aspect ratio across all sheets.
- Keep stable character names and visual descriptors across prompts.
- Carry over setting, props, wardrobe, color, and design language unless the story intentionally changes.
- Use clear shot language: establishing shot, close-up, over-the-shoulder, tracking shot, insert shot, wide shot, montage, etc.
- Make each page visibly read as a storyboard sheet, not a poster or a single full-frame illustration.
- Never put all requested sheets into one combined image.
- Never generate alternate versions of the same sheet when the user asked for multiple sheets.

If reference images are provided, identify the important visual features and carry them through all prompts. If the reference is a storyboard layout, match its structure. If reference text is provided, adapt the sequence to it instead of replacing it with a new story.

## Prompt Pattern

Use this structure for each sheet prompt:

```text
Storyboard sheet [sheet number] of [total sheets], [aspect ratio]. Generate this as one complete storyboard page image, not a combined set of all pages.
Layout: header, concept line, numbered cut cards in a clean grid, each cut with image area plus ACTION/DIALOGUE/TEXT rows, optional notes box.
Continuity: [stable characters, wardrobe, props, setting, palette, style, previous sheet ending].
Sheet story: [what this sheet covers and how it connects to previous/next sheet].
Cuts: [exact cut numbers for this sheet only, titles, actions, dialogue/narration, text, shot types].
Mood and lighting: [specific mood, light, color].
Style: [requested or inferred style], cinematic storyboard sheet, coherent sequence, clean readable production layout, no random extra characters, no watermark.
```

For sheet 2 and later, the prompt must include: "Sheet [N] continues after cut [previous final cut]. Cuts on this page are [start]-[end]." Example: "Sheet 2 continues after cut 06. Cuts on this page are 07-12."

## Response Workflow

After the user answers the intake questions:

1. Summarize style, references, sheet count, cuts-per-sheet assumption, and aspect ratio.
2. Present the continuity plan and sheet-by-sheet cut list.
3. Generate each storyboard sheet image separately and in order.
4. Return the images with exact cut descriptions in text.
5. Offer continuation or revision options while preserving continuity.

When the user asks to continue an existing storyboard, reuse the continuity bible and previous final cut as the starting state. Ask only for the number of additional sheets and any new direction if missing.

## Defaults

- Aspect ratio: 16:9.
- Sheet count: ask before generating unless specified.
- Cuts per sheet: infer 6 or 8 when omitted.
- Style: ask first; if the user wants draft mode, infer from the brief.
- Output: separate connected storyboard sheet images, ordered by sheet number.
- Language: respond in the user's language.

## Safety And Portability

Do not include local usernames, absolute machine paths, private account details, API keys, or hidden metadata in generated prompts or saved skill files.
