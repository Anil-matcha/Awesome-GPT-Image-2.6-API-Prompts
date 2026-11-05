# Awesome GPT-Image-2.6 Prompts

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](LICENSE)

A curated collection of prompts, techniques, and API notes for **ChatGPT Images 2.6** — OpenAI's image update released November 4, 2026 — and its API models **GPT-Image-2.6 Flare** and **GPT-Image-2.6 Sunburst**. This repository tracks what is new in 2.6 (animated GIF output, image markup, SVG export, a `complexity` setting, and faster generation) and collects prompt patterns tuned to those features.

Whether you are building an image app, upgrading a `gpt-image-2.5` integration, or looking for prompts that make the most of GIFs and markup edits, you will find practical patterns here.

> **Want GPT Image models without an OpenAI account?** **[MuAPI](https://muapi.ai)** hosts them behind one REST API and one key. GPT Image 2.6 Flare and Sunburst (text-to-image and image editing, up to 4K, animated GIF output) are available at [muapi.ai/gpt-image-2.6](https://muapi.ai/gpt-image-2.6), and [GPT Image 2.5 Flare and Sunburst](https://muapi.ai/gpt-image-2.5) remain available too. [Get your API key →](https://muapi.ai)

> **API usage:** Prompts below are written for the [OpenAI Images API](https://developers.openai.com/api/docs/guides/image-generation) using `gpt-image-2.6-flare` / `gpt-image-2.6-sunburst`, and most also work in ChatGPT Images 2.6. Check OpenAI's docs for the exact parameter names and values before shipping; they are quoted here from the launch post and image-generation guide as of 2026-11-05.

```python
import openai

client = openai.OpenAI()
response = client.images.generate(
    model="gpt-image-2.6-flare",   # or gpt-image-2.6-sunburst for the quality tier
    prompt="<paste any prompt from this list>",
    size="1024x1024",
    quality="high",
    n=1,
)
```

---

## Related Projects

- [MuAPI GPT Image 2.6 landing page](https://muapi.ai/gpt-image-2.6) — Flare and Sunburst live on Muapi (text-to-image and image editing, up to 4K, GIF output, from $0.06/image).
- [MuAPI GPT Image 2.5 API](https://muapi.ai/gpt-image-2.5) — Flare and Sunburst 2.5 live on Muapi today.
- [MuAPI API reference](https://muapi.ai/docs/api-reference) — Endpoint and prediction lifecycle documentation.
- [Awesome-GPT-Image-2.5-API-Prompts](https://github.com/Anil-matcha/Awesome-GPT-Image-2.5-API-Prompts) — The prior-generation prompt collection this repo builds on.
- [Awesome-GPT-Image-2-API-Prompts](https://github.com/Anil-matcha/Awesome-GPT-Image-2-API-Prompts) — GPT-Image-2 prompts.
- [Generative-Media-Skills](https://github.com/SamurAIGPT/Generative-Media-Skills) — Run these prompts as AI agent skills in Claude Code, Cursor, and Gemini CLI.
- [muapi-cli](https://github.com/SamurAIGPT/muapi-cli) — Run image-generation prompts via CLI with MuAPI.
- [Open-Generative-AI](https://github.com/Anil-matcha/Open-Generative-AI) — Open-source generative media studio covering image, video, and audio generation.
- [awesome-ai-image-models](https://github.com/Anil-matcha/awesome-ai-image-models) — Compare AI image models by API, price & quality.

## What's New in 2.6

Per [OpenAI's announcement](https://openai.com/index/introducing-images-2-6/):

- **Animated GIFs** — animate a brand mascot, make reaction memes, storyboard a character's movement, or turn a sketch into an animated character
- **Image markup in the API** — previously ChatGPT-only; mark up the image to pinpoint exactly where a change should happen
- **SVG export** — vector output intended for websites, apps, and print
- **`complexity` setting** — controls how much the model plans before drawing. `quality` is detail and fidelity; `complexity` is how much goes into the scene
- **50% faster** than before; Flare can generate in as little as six seconds at `quality=low`
- Two API tiers: **Flare** (fast iteration, improved layout quality for posters, product imagery, professional visuals) and **Sunburst** (higher quality and more consistency across edits at medium and high quality)

### API notes (from OpenAI's image-generation guide)

| Topic | Detail |
|---|---|
| GIF endpoint | Image API **generations** endpoint only — the edit endpoint does not support GIF |
| `frame_count` | 2–64 (default 9) |
| `frame_duration_ms` | 20–2000, rounded to 10 (default 200) |
| `complexity` | Supported by both models. OpenAI recommends low for most edits, medium/high for scenes with many elements |
| Markup, SVG, GIF | Supported by both Flare and Sunburst through the Image API |
| Sunburst token pricing | Text in $5 / 1M (cached $1.25), image in $8 / 1M (cached $2), image out $30 / 1M — same as 2.5 |

Prompts below are community-style starting points, not OpenAI-published examples. Results vary; test on both tiers.

---

## Table of Contents

- [Animated GIFs](#animated-gifs)
- [Markup-Guided Edits](#markup-guided-edits)
- [SVG & Vector Graphics](#svg--vector-graphics)
- [Complexity: Low vs High](#complexity-low-vs-high)
- [Posters & Product Imagery (Flare)](#posters--product-imagery-flare)
- [Multi-Round Edit Consistency (Sunburst)](#multi-round-edit-consistency-sunburst)
- [Resources & API Docs](#resources--api-docs)
- [Contributing](#contributing)

---

## Animated GIFs

Use the generations endpoint with a frame count and frame duration. Describe the motion as a sequence so each frame differs predictably. Short loops (6–12 frames) work best.

### Looping Brand Mascot

**Prompt:**
```
A looping animated GIF of a friendly round teal robot mascot waving its right arm: frame 1 arm down, middle frames arm raised and swinging side to side, final frame returning to arm down so the loop is seamless. Flat vector style, clean white background, identical character proportions and colors in every frame.
```

### Reaction Meme

**Prompt:**
```
An animated reaction GIF of a cartoon cat slowly turning from a calm expression to wide-eyed shock, then a small "WAIT, WHAT?" caption popping in at the end. Bold outlines, pastel background, consistent character design across all frames.
```

### Animated Storyboard Beat

**Prompt:**
```
An animated storyboard GIF of a paper boat drifting across a puddle: boat enters from the left, ripples expand beneath it, boat exits to the right. Soft watercolor look, overhead camera, same puddle and lighting in every frame.
```

### Typing-Indicator Character

**Prompt:**
```
A tiny looping GIF of a cute blob character bouncing three times as if typing, simple two-color palette, transparent-looking pastel background, same character shape and size in every frame.
```

### Sketch to Animated Character

Attach a hand-drawn sketch where your client supports it.

**Prompt:**
```
Turn the attached hand-drawn sketch into an animated character GIF: keep the sketch's shape and line quality, add a gentle idle animation (blinking, slight head tilt), consistent proportions in all frames, plain background.
```

---

## Markup-Guided Edits

Markup lets you point at the region to change. Pair the markup with a prompt that names what changes and what must stay fixed.

### Change Only the Marked Region

**Prompt:**
```
In the area I marked on the attached image, replace the object with a vintage brass desk lamp. Keep the lighting direction, shadows, perspective, and everything outside the marked area exactly as in the original.
```

### Fix a Marked Text Block

**Prompt:**
```
Inside the marked box on the poster, change the text to "OPEN LATE FRIDAYS" in the same font, weight, and color. Do not change any other element of the layout.
```

### Remove a Marked Distraction

**Prompt:**
```
Remove the object inside the marked circle and fill the area so it matches the surrounding texture and lighting seamlessly. Leave the rest of the image untouched.
```

---

## SVG & Vector Graphics

Ask for flat shapes, limited palettes and clear edges so the result converts cleanly to vector output.

### App Icon Set

**Prompt:**
```
A set of four flat app icons — camera, calendar, chat bubble, map pin — in one consistent style: rounded squares, two-tone gradient fills, thick uniform strokes, no shadows, centered on a plain background. Clean geometric shapes suitable for vector export.
```

### Logo Mark

**Prompt:**
```
A minimalist logo mark for a coffee roaster: a stylized coffee bean formed from two overlapping crescents, single accent color on white, crisp edges, no gradients, no texture, suitable for SVG.
```

### Print-Ready Pattern Tile

**Prompt:**
```
A seamless repeating pattern of geometric leaves in sage green and cream, flat colors only, even spacing, crisp edges, designed to tile for print and web backgrounds.
```

---

## Complexity: Low vs High

Per OpenAI, keep `complexity` low for most edits and raise it for crowded scenes with many constraints.

### Low Complexity: Simple Product Edit

**Prompt:**
```
Change the color of the sneaker in the attached photo from white to matte black. Keep the laces, sole, lighting, and background identical.
```

### High Complexity: Crowded Scene With Constraints

**Prompt:**
```
A busy night-market street scene: exactly five food stalls, each with a distinct sign (noodles, dumplings, skewers, tea, desserts), a cyclist in the foreground, lanterns overhead in alternating red and gold, wet pavement reflecting the lights, and a distant skyline. Keep every stall's sign legible and the lantern colors strictly alternating.
```

---

## Posters & Product Imagery (Flare)

Flare targets fast iteration with improved layout quality. Use it for drafts, then finish on Sunburst.

### Event Poster

**Prompt:**
```
A bold event poster for "NIGHT MARKET 2026": large condensed headline at the top, date and location line below, a central illustration of lantern-lit stalls, strong grid alignment, three-color palette of deep navy, warm orange, and cream, generous margins.
```

### Product Hero Shot

**Prompt:**
```
A studio hero shot of a matte ceramic mug on a marble counter: soft window light from the left, subtle steam, shallow depth of field, clean negative space on the right for headline copy.
```

---

## Multi-Round Edit Consistency (Sunburst)

Sunburst is positioned for more consistency across edits at medium and high quality. Run edits as a chain and check that earlier changes survive.

### Character Across Three Edits

**Turn 1:**
```
Generate a full-body character sheet of a young explorer: olive jacket, red scarf, brown boots, short curly hair.
```
**Turn 2:**
```
Keep the same character exactly and change only the scarf to mustard yellow.
```
**Turn 3:**
```
Keep the same character and the yellow scarf, and add a small canvas backpack. Change nothing else.
```

---

## Resources & API Docs

- [OpenAI: Introducing ChatGPT Images 2.6](https://openai.com/index/introducing-images-2-6/)
- [OpenAI image generation guide](https://developers.openai.com/api/docs/guides/image-generation)
- [MuAPI GPT Image 2.6 page](https://muapi.ai/gpt-image-2.6) · [GPT Image 2.5 on Muapi](https://muapi.ai/gpt-image-2.5)
- [MuAPI documentation](https://muapi.ai/docs/introduction)

## Contributing

Pull requests welcome. Add prompts you have actually tested, state which tier (Flare or Sunburst) and settings you used, and keep claims tied to OpenAI's documentation.
