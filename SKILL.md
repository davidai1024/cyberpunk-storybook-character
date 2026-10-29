---
name: cyberpunk-storybook-character
description: Generate an original cyberpunk storybook character in a retro-futurist animation cel style from an object, animal, person, profession, mood, action, or combined phrase. Use for stylized cel-shaded sci-fi characters with integrated cybernetic details; output one isolated character on a pure-white PNG canvas.
---

# Cyberpunk Storybook Character

Generate exactly one isolated, cyberpunk-inflected author-led storybook character in a retro-futurist animation cel style from the user's complete input. The default output is a cel-shaded 2.5D-style PNG image, not an actual 3D mesh or animation. If a model or turntable is explicitly requested, route to a capable 3D workflow and verify the requested asset or animation separately.

## Core invariant

Every generation must use:

1. The same master prompt below.
2. Two changing fields: the user's exact `{{USER_INPUT}}` and a deterministic `{{PALETTE_DIRECTIVE}}` calculated from that input.
3. A retro-futurist animation cel character with fine dark contours, clear flat color fields and two or three crisply separated cel-shadow shapes, with integrated cybernetic construction. Retain the original's distinctive storybook silhouette and understated expression; suggest depth through graphic planes, not photorealistic 3D.

Never add subject-specific design instructions, including proposed silhouette, pose, anatomy, negative-space solution, facial layout, prop placement, manually chosen color palette, or exaggeration method. The purpose of this Skill is to let the same artistic method discover a different structural answer for any input while the deterministic palette mechanism prevents repeated default colorways.

## Deterministic palette mechanism

Before every generation, calculate a palette directive from the exact UTF-8 bytes of `{{USER_INPUT}}`:

1. Compute SHA-256 of the exact input.
2. Let `A`, `B`, `C`, `D`, and `E` be the decimal values of the first five hash bytes.
3. Calculate:
   - `H1 = A × 360 // 256`
   - `H2 = (H1 + 47 + B % 127) % 360`
   - `H3 = (H2 + 47 + C % 127) % 360`
   - `S1 = 58 + D % 31`, `S2 = 52 + E % 35`, `S3 = 66 + B % 25`
   - `L1 = 36 + C % 29`, `L2 = 48 + D % 27`, `L3 = 42 + E % 31`
4. Fill `{{PALETTE_DIRECTIVE}}` with exactly:

```text
Use this computed one-run palette: dominant HSL(H1 S1% L1%), secondary HSL(H2 S2% L2%), accent HSL(H3 S3% L3%). Keep the dominant color visibly predominant and use the other two sparingly. These numeric colors are binding. Do not substitute a familiar default palette.
```

5. Replace the symbols with the calculated integers before generation.
6. If the user explicitly specifies one or more colors, those explicit colors remain binding; use the computed colors only for unspecified roles.

## Context isolation

Every invocation is context-independent.

- Use only the user's current complete input and this Skill file.
- Do not use prior conversation, earlier generations, prior assistant interpretations, remembered palettes, recently used shapes, or previous outputs as generation context.
- Do not inspect, reference, compare with, imitate, or continue any image generated in an earlier invocation.
- Do not add inferred details from earlier turns, even when the current input resembles a previous subject.
- Do not use any image reference unless the user explicitly supplies one in the current request and explicitly asks for reference-based generation.

## Input interpretation

- Treat the user's entire phrase as one unified character concept.
- Never split comma-separated keywords into multiple characters unless the user explicitly requests multiple separate outputs.
- If the user explicitly lists several independent subjects and requests one image for each, run the identical master prompt separately for every subject, changing `{{USER_INPUT}}` and its computed `{{PALETTE_DIRECTIVE}}`.
- Preserve explicit attributes in the input, such as color, species, profession, action, mood, or object type.
- Express cyberpunk through purposeful features integrated into the character's structure, not a repeated accessory. Optional metallic highlights must remain subtle, graphic accents; avoid realistic reflections, clay-like surfaces and neon glass.

## Generation settings

Use `generate_image` with:

- `aspect`: `1:1`
- `size`: `4K`
- no `ref`
- one final PNG per subject under `/home/user/workspace/outputs/<task-name>/`

The generated image must be a complete isolated character on an opaque, uniform pure-white (#FFFFFF) canvas. Never request a transparent background, background removal, or a simulated transparency checkerboard. Do not add grids, gray squares, off-white paper, or background texture.

Do not mention SVG, vector, editable paths, icons, logos, or vectorization in the image-generation prompt. These words distort the visual language toward rigid vector mascots. Output PNG only by default. If true SVG is explicitly requested, treat it as a separate vector-production task and verify actual vector paths; never rename a PNG to .svg or embed a PNG in an SVG wrapper and describe it as vector artwork.

## Master prompt

Replace only `{{USER_INPUT}}` and `{{PALETTE_DIRECTIVE}}`. Do not modify, expand, paraphrase, or append subject-specific visual solutions.

```text
Create one isolated original cyberpunk storybook character based only on this complete user input: “{{USER_INPUT}}”. Render it as a sophisticated retro-futurist animation character using traditional hand-painted animation cel aesthetics. Use confident, fine dark contour lines, broad flat color fields, and two or three crisply separated cel-shadow shapes. Suggest modest 2.5D depth through graphic planes rather than realistic rendering. Preserve an independent storybook artist's inventive shapes, quiet expression, and naturally humorous sensibility, infused with a clear, inventive cyberpunk identity. Do not derive anything from prior conversation, earlier images, remembered palettes, recently used shapes, or previous outputs.

Interpret the complete input as one unified character concept. Preserve its essential identity, function, mood, profession, and explicitly implied attributes, but do not solve it by placing accessories onto a conventional mascot body. Recognition should come from a few decisive cues. First invent the primary silhouette, then allow proportion, posture, structural integration, asymmetrical balance, and meaningful negative space to carry the imagination. Let professional, functional, emotional, animal, plant, or object qualities reshape the body itself when useful. Find a fresh structural answer appropriate only to this subject; do not use a standard body template, standard species anatomy, or a predetermined exaggeration formula. Express cyberpunk through a small number of organically integrated futuristic or cybernetic forms, technological seams, modular structures, or compact electronic details that emerge from the character itself. Select and invent these in response to the subject; do not automatically repeat the same headset, visor, implants, clothing, or props across characters.

Keep the character quiet, observant, slightly unusual, and naturally humorous. Facial features, if present, should be understated. Make its cybernetic construction part of the body itself through a few intentional, subject-appropriate seams, engineered elements or small electronic insets, not a generic costume or a pile of accessories. Keep the shape language elegant, imaginative and recognizable. Use clean, decisive flat colors, fine dark lines and crisp cel-shading; use a few restrained graphic metallic highlights only where they help describe the integrated technology. Keep large color areas clean and mostly flat, with no realistic surface reflections or detailed material simulation. Keep the background absolutely white, with no cast shadow or floor.

{{PALETTE_DIRECTIVE}}

Show exactly one complete, uncropped character centered with comfortable empty padding on an opaque, flat, uniform pure-white (#FFFFFF) background extending to every canvas edge. The background must be actual solid white, not transparency or a transparency preview. No checkerboard, grid, gray squares, off-white or ivory backdrop, paper texture, background gradient, scenery, ground plane, frame, badge, circle, cast shadow, shadow panel, caption, label, logo, or typography.

Avoid cyberpunk cityscapes, night scenes, glowing halos, weapon-centric designs, generic sci-fi armor, and repeated accessory formulas. Avoid photorealism, full 3D figurine render, realistic 3D product photography, sculptural airbrushed shading over the whole body, neon glass, mirror chrome, harsh glare, excessive reflections, standardized mascot anatomy, identical round heads, default arms and legs, oversized glossy eyes, generic cute-cartoon styling, conventional species silhouettes when a more inventive but recognizable construction is possible, pasted-on surreal accessories, polished geometric symmetry, heavy black outlines, clay, plasticine, ceramic, rubber, vinyl-toy or waxy soft-plastic surfaces, fingerprints, muddy shading, stains, speckles, mottling, grain, distressed wear, or dirty overlays. The final image should feel immediately readable yet structurally surprising, like a distinctive cyberpunk character from an animated storybook.
```

## Quality check

Before delivery, verify:

- Exactly one character per output.
- Complete silhouette is visible and uncropped.
- Canvas is opaque and uniformly pure white (#FFFFFF), with no checkerboard, grid, gray squares, transparency, off-white tint, texture, gradient, or shadow.
- The requested subject remains immediately recognizable.
- Structural imagination comes from silhouette, proportion, posture, integration, or negative space.
- The character reads as a hand-painted animation cel: fine dark contours, broad flat color fields, and two or three crisp graphic shadow planes suggest modest depth. Reject photorealistic 3D, toy-like or clay-like rendering.
- Cybernetic components or seams are visibly integrated into the subject's form. Optional metallic highlights are sparse graphic accents, not realistic chrome, glass or detailed physical texture.
- Color areas are clean and vivid; cel shadows remain crisp and distinct without dirty or mottled texture.
- The prompt contains the correctly calculated HSL directive for the exact current input.
- The delivered image visibly follows the computed dominant hue rather than a familiar default palette.
- Cyberpunk is visibly present in integrated futuristic construction and materials while the original storybook character language remains dominant; no default neon glass, generic repeated accessories, background halo, dark scene, or city background.
- The result is not a generic cute mascot or rigid vector icon.

If a result fails, rerun with the exact same master prompt and input. Do not repair it by adding subject-specific design instructions. If a repeated attempt still fails, report the specific limitation honestly; never describe an off-white background as strictly pure white or claim an unverified output property.

## Delivery

Deliver each PNG separately and describe it accurately as an animation-cel-style character image. Describe the background as pure white only after it passes the white-background check. Do not claim the PNG is a real 3D model, has transparency, background removal, SVG output, or vector editability. Never present a renamed PNG or an SVG containing an embedded bitmap as a true vector SVG.
