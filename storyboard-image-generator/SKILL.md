---
name: a1-storyboard-maker
description: Create sequential storyboard sheets or consistent character-sheet images from a user's idea, script, article, character description, or visual reference. Use when Codex should route the request to option 1 storyboard or option 2 character sheet, ask only for missing references, image count, and aspect ratio, then generate one or more production-ready sheets. Storyboard pages must continue across sheets; character sheets must preserve the same character identity across views and pages.
---

# A1 Storyboard And Character Sheet Maker

This skill has two modes:

1. Storyboard
2. Character sheet

## Route The Request First

Determine the mode from the user's request before asking questions.

- Use option 1 when the user asks for a storyboard, scene sequence, shot plan, cuts, panels, ad sequence, video plan, or connected story pages.
- Use option 2 when the user asks for a character sheet, model sheet, turnaround, expression sheet, pose sheet, character reference board, or consistent multi-view character design.
- If the request clearly matches one mode, proceed with that mode. Do not ask the user to choose again.
- If the request is unclear or does not clearly match either mode, ask:

```markdown
어떤 작업을 원하시나요?

1. 스토리보드
2. 캐릭터 시트
```

Do not mix both modes unless the user explicitly requests both.

# Option 1: Storyboard

Turn a user brief into connected storyboard sheet images. Preserve continuity across every sheet and cut: characters, wardrobe, props, setting, camera language, aspect ratio, mood, and visual style.

## Absolute Storyboard Rule

Multiple storyboard sheets are one continuing story split across pages.

- Never treat multiple sheets as different versions, options, drafts, or variations.
- Never generate the same sheet number twice unless the user explicitly asks for variants.
- Generate sheet 1, then sheet 2, then sheet 3, in order.
- Each later sheet must continue directly from the final cut of the previous sheet.
- Cut numbers must continue across sheets.
- If sheet 1 has cuts 01-06, sheet 2 must have cuts 07-12.
- If sheet 1 has cuts 01-08, sheet 2 must have cuts 09-16.
- If the user says "2장만 만들어", create two sequential storyboard pages, not two alternate images.

## Storyboard Intake

Ask only for information that is still missing:

1. Reference material: script, article, treatment, image, storyboard sample, character description, or visual reference.
2. Storyboard style: cinematic, webtoon, commercial pitch, rough pencil, animation board, product ad, documentary, etc.
3. Number of storyboard sheets.
4. Cuts per sheet, if the user cares. If omitted, infer 6 or 8 based on story density.
5. Aspect ratio. Default to 16:9.

If the user already supplied enough information, proceed without repeating these questions.

## Storyboard Planning

Before generating images, create:

1. Story premise in one sentence.
2. Visual style: medium, mood, palette, detail level, and lighting.
3. Continuity bible: recurring characters, wardrobe, props, setting, time of day, and reference constraints.
4. Exactly the requested number of sheets.
5. A continuous cut list across every sheet.
6. Aspect ratio: user requested ratio, otherwise 16:9.

Example for two sheets with six cuts each:

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
- 08컷 [상황 확장]
- 09컷 [핵심 선택 또는 위기]
- 10컷 [해결 방향]
- 11컷 [결과 또는 공개]
- 12컷 [마무리 또는 다음 시퀀스 연결점]
```

Plan all requested sheets before generating the first image.

## Storyboard Layout

When no layout reference is provided:

- Header: `STORYBOARD | [project title]`.
- Numbered cut cards in a readable grid.
- Each card includes an image, cut number, short title, shot type, ACTION, DIALOGUE, and TEXT.
- Add a notes box only when useful.
- Use Korean labels when the user writes in Korean.
- Also provide exact cut descriptions in chat because generated small text may be imperfect.

## Storyboard Generation

- Generate one separate image per sheet.
- Use unique sheet numbers: sheet 1 of N, sheet 2 of N, and so on.
- Continue cut numbers across sheets.
- For sheet 2 and later, state the previous final cut and the new cut range.
- Keep the same aspect ratio and visual continuity across all sheets.
- Never combine every requested sheet into one image.
- Never generate alternate versions when the user asked for sequential sheets.

Use this prompt structure:

```text
Storyboard sheet [sheet number] of [total sheets], [aspect ratio].
Generate one complete production storyboard page.
Layout: [header, grid, cut cards, ACTION/DIALOGUE/TEXT rows].
Continuity: [characters, wardrobe, props, setting, palette, style, previous ending].
Sheet story: [coverage and connection to previous/next sheet].
Cuts: [exact cut numbers and shot descriptions for this sheet].
Mood and lighting: [specific direction].
No unrelated characters, no watermark.
```

For later pages include: `Sheet 2 continues after cut 06. Cuts on this page are 07-12.`

# Option 2: Character Sheet

Create production-ready character reference sheets from a written description, uploaded reference image, or both. Preserve the character's identity, proportions, face, hairstyle, costume, materials, accessories, and palette across every view and every generated sheet.

## Character Sheet Intake

Ask only for missing information:

1. Character description or reference image.
2. Desired visual style, if not clear from the reference or description.
3. Number of character-sheet images to generate.
4. Aspect ratio. Default to 16:9.

If the user supplies a reference image, analyze and preserve its defining traits. Do not merely copy the reference pose; use it to create a consistent multi-view design.

If only a short description is provided, expand it conservatively into a coherent character design and state the key assumptions before generating.

## Character Identity Bible

Before generation, summarize:

- Name or working label.
- Age range and role.
- Body type and proportions.
- Face shape, skin tone, eyes, eyebrows, nose, lips, and distinctive marks.
- Hair shape, length, texture, and color.
- Clothing silhouette, layers, materials, colors, and footwear.
- Accessories, props, symbols, and small identifying details.
- Art style, line/detail level, lighting, and palette.
- Requested sheet count and aspect ratio.

Use the same identity bible in every character-sheet prompt.

## Default Character Sheet Layout

Use a clean, light neutral production-board background with thin dividers and restrained labels. Adapt the layout to the character, but include as many of these as the page can clearly support:

- Large title and `CHARACTER SHEET` subtitle.
- Turnaround views: front, 3/4 front, profile, and back.
- Large hero portrait, usually a 3/4 view.
- Expression studies such as neutral, gentle smile, thoughtful, surprised, angry, sad, or user-requested emotions.
- Detail close-ups for accessories, costume materials, patterns, tools, scars, tattoos, or signature features.
- Color palette swatches with short labels.
- Compact character metadata: name, age range, role, origin/world, personality notes, and costume notes.

For a full-body design, prioritize full-body front, side, 3/4, and back views. For a portrait-focused reference, prioritize head-and-shoulder turnarounds, expressions, and facial details.

Keep labels short and legible. Also provide the exact character specifications in chat because generated text may be imperfect.

## Multiple Character Sheets

Generate one separate image per requested sheet.

- Keep the same character identity across all sheets unless the user explicitly asks for different variants.
- Do not create duplicate pages.
- Sheet 1 should normally establish the core turnaround, hero portrait, palette, and essential details.
- Additional sheets should expand useful coverage: expressions, action poses, hand studies, costume layers, alternate approved outfits, equipment, scale comparisons, or additional detail close-ups.
- If the user explicitly requests design variations, label each variation clearly and keep the requested invariant traits stable.

## Character Sheet Generation

- Use the user's requested ratio for every image; otherwise use 16:9.
- Match the reference's medium and design language when supplied.
- Keep face, body proportions, hairstyle, costume construction, accessories, and colors consistent.
- Use neutral, readable lighting unless dramatic lighting is part of the requested design.
- Avoid random wardrobe changes, mirrored asymmetrical details, missing accessories, duplicate limbs, unrelated characters, and watermarks.
- Make the output read as a professional model sheet, not a collage of unrelated portraits.

Use this prompt structure:

```text
Character sheet [sheet number] of [total sheets], [aspect ratio].
Create one complete professional character reference page.
Character identity: [stable identity bible].
Layout: [turnarounds, hero portrait, expressions, detail close-ups, palette, metadata].
Sheet focus: [core turnaround or additional coverage].
Views and studies: [exact views, expressions, poses, and details].
Style: [requested medium and visual language].
Use a clean neutral production-board background, consistent scale and identity, short readable labels, no unrelated characters, no watermark.
```

## Response Workflow

For either mode:

1. Identify the selected option.
2. Ask only for missing inputs.
3. Summarize references, assumptions, image count, and aspect ratio.
4. Present a compact plan before generation.
5. Generate each requested image separately and in order.
6. Return each image with readable text specifications.
7. Preserve continuity when revising or extending existing work.

## Defaults

- Default aspect ratio: 16:9.
- Default language: the user's language.
- Storyboard cuts per sheet: infer 6 or 8 when omitted.
- Character-sheet image count: ask when omitted.
- Output: separate image files, one per requested sheet.

## Safety And Portability

Do not include local usernames, absolute machine paths, private account details, API keys, or hidden metadata in prompts or saved skill files.
