---
name: cyberpunk-storybook-character
description: Generate an original cyberpunk storybook character in retro-futurist animation cel style from an object, animal, person, profession, mood, action, or combined phrase; output one isolated character on a white PNG canvas.
---

# Cyberpunk Storybook Character

Generate one original character per image using the fixed master prompt below. The result is a cel-shaded 2.5D-style PNG illustration, not a 3D model or animation; route explicit model or turntable requests to an appropriate 3D workflow.

## Input and isolation

Treat the user's complete phrase as one concept, preserving explicit attributes. Split subjects only when separate images are explicitly requested; run the same prompt independently for each. Use only the current complete input and this Skill: do not use prior conversation, previous images, remembered palettes or inferred details. Do not use an image reference unless the user supplies it in the current request and explicitly asks to use it.

Change only `{{USER_INPUT}}` and its computed `{{PALETTE_DIRECTIVE}}` in the master prompt. Do not append subject-specific silhouettes, poses, anatomy, props, colors or other design solutions.

## Deterministic palette

Hash the exact UTF-8 bytes of `{{USER_INPUT}}` with SHA-256. Let A–E be the first five bytes as integers and calculate:

- H1 = A × 360 // 256; H2 = (H1 + 47 + B % 127) % 360; H3 = (H2 + 47 + C % 127) % 360
- S1 = 58 + D % 31; S2 = 52 + E % 35; S3 = 66 + B % 25
- L1 = 36 + C % 29; L2 = 48 + D % 27; L3 = 42 + E % 31

Replace the symbols in the following directive with the computed integers:

```text
Use this computed one-run palette: dominant HSL(H1 S1% L1%), secondary HSL(H2 S2% L2%), accent HSL(H3 S3% L3%). Keep the dominant color visibly predominant and use the other two sparingly. These numeric colors are binding. Do not substitute a familiar default palette.
```

Explicit user colors remain binding; use computed colors only for unspecified roles.

## Generation

Use `generate_image` with aspect `1:1`, size `4K`, no reference by default, and one final PNG per subject under `/home/user/workspace/outputs/<task-name>/`. When a reference is explicitly supplied and requested, use it for the requested reference-based generation. The character must be complete on an opaque, uniform pure-white (#FFFFFF) background, not transparency, a checkerboard or a textured backdrop. Do not put SVG, vector, editable paths, icons, logos or vectorization in the generation prompt. True SVG or actual 3D requests require separate capable workflows and verification; never label an embedded or renamed PNG as a vector asset.

## Master prompt

Replace only the two fields; do not modify the prompt or add subject-specific instructions.

```text
Create one isolated original cyberpunk storybook character based only on this complete user input: “{{USER_INPUT}}”. Render it as a sophisticated retro-futurist animation character using traditional hand-painted animation cel aesthetics. Use confident, fine dark contour lines, broad flat color fields, and two or three crisply separated cel-shadow shapes. Suggest modest 2.5D depth through graphic planes rather than realistic rendering. Preserve an independent storybook artist's inventive shapes, quiet expression, and naturally humorous sensibility, infused with a clear, inventive cyberpunk identity. Do not derive anything from prior conversation, earlier images, remembered palettes, recently used shapes, or previous outputs.

Interpret the complete input as one unified character concept. Preserve its essential identity, function, mood, profession, and explicitly implied attributes, but do not solve it by placing accessories onto a conventional mascot body. Recognition should come from a few decisive cues. First invent the primary silhouette, then allow proportion, posture, structural integration, asymmetrical balance, and meaningful negative space to carry the imagination. Let professional, functional, emotional, animal, plant, or object qualities reshape the body itself when useful. Find a fresh structural answer appropriate only to this subject; do not use a standard body template, standard species anatomy, or a predetermined exaggeration formula. Express cyberpunk through a small number of organically integrated futuristic or cybernetic forms, technological seams, modular structures, or compact electronic details that emerge from the character itself. Select and invent these in response to the subject; do not automatically repeat the same headset, visor, implants, clothing, or props across characters.

Keep the character quiet, observant, slightly unusual, and naturally humorous. Facial features, if present, should be understated. Make its cybernetic construction part of the body itself through a few intentional, subject-appropriate seams, engineered elements or small electronic insets, not a generic costume or a pile of accessories. Keep the shape language elegant, imaginative and recognizable. Use clean, decisive flat colors, fine dark lines and crisp cel-shading; use a few restrained graphic metallic highlights only where they help describe the integrated technology. Keep large color areas clean and mostly flat, with no realistic surface reflections or detailed material simulation. Keep the background absolutely white, with no cast shadow or floor.

{{PALETTE_DIRECTIVE}}

Show exactly one complete, uncropped character centered with comfortable empty padding on an opaque, flat, uniform pure-white (#FFFFFF) background extending to every canvas edge. The background must be actual solid white, not transparency or a transparency preview. No checkerboard, grid, gray squares, off-white or ivory backdrop, paper texture, background gradient, scenery, ground plane, frame, badge, circle, cast shadow, shadow panel, caption, label, logo, or typography.

Avoid cyberpunk cityscapes, night scenes, glowing halos, weapon-centric designs, generic sci-fi armor, and repeated accessory formulas. Avoid photorealism, full 3D figurine render, realistic 3D product photography, sculptural airbrushed shading over the whole body, neon glass, mirror chrome, harsh glare, excessive reflections, standardized mascot anatomy, identical round heads, default arms and legs, oversized glossy eyes, generic cute-cartoon styling, conventional species silhouettes when a more inventive but recognizable construction is possible, pasted-on surreal accessories, polished geometric symmetry, heavy black outlines, clay, plasticine, ceramic, rubber, vinyl-toy or waxy soft-plastic surfaces, fingerprints, muddy shading, stains, speckles, mottling, grain, distressed wear, or dirty overlays. The final image should feel immediately readable yet structurally surprising, like a distinctive cyberpunk character from an animated storybook.
```

## Verify and deliver

Check each output for one recognizable, complete character; inventive silhouette and integrated cybernetic details; fine dark contours, broad clean color fields, two or three crisp cel-shadow shapes, subdued expression and subtle graphic metallic accents; the computed palette, particularly its dominant hue; and an opaque, uniform pure-white (#FFFFFF) background with no shadow or scenery. Reject photorealistic, toy-like, clay-like, neon-glass, generic mascot or heavily reflective results.

If any check fails, rerun with the exact same prompt and input without adding subject-specific instructions. If a repeat still fails, report the limitation honestly; do not call a near-white background pure white. Deliver each PNG separately as a cel-animation-style character image. Do not claim transparency, SVG, editable paths or 3D assets without separately verifying them.
