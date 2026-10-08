# Card prompts: clane

## front

カードの表。ストーリーと同じボタニカルアートの画風で、そのおりがみの動物を描く。

### style

Vertical illustration in playing-card proportions (5:7). A blend of an antique botanical plate and a natural-history animal illustration: precise, fine ink outlines, delicate cross-hatching, and meticulous colored-pencil shading. Leaf veins, petals, stems, fur, and feathers are carefully rendered. A subtle texture of off-white paper. A palette of plant greens, ochre, grey-blue, and cream, with small, restrained accents of red and blue. A quiet beauty that children can understand and adults can appreciate.

### character

The crane: a red-crowned crane with natural proportions, carrying a small ochre shoulder bag on a strap. Natural anatomy, small eyes, closed beak, nearly neutral expression.

### scene

The crane stands tall and still on one spot, its long neck upright, seen from the side, its whole body from head to feet visible. Tall reeds, sedges, and a low branch of Japanese red pine frame the crane; the ground at its feet is a shallow, still waterside.

### composition

A single animal portrait centered on the card, filling most of its height, with plants arranged naturally around it as in a botanical plate. Leave a quiet margin of off-white paper around the edges. Even, soft light.

### constraints

No watercolor bleeding or blur, no impasto, no glossy digital painting, no 3D rendering. No large eyes, no cartoon faces, no baby-like proportions, no exaggerated gestures. Only the one animal described appears. No text, labels, numbers, card corner symbols, frames, borders, watermarks, or signatures.

## back

カードの裏。折り上がったおりがみの画像。完成形がほぼ決まっているので先に作る。`steps/` の折り方のデータができた後、形が違っていたら作り直す。

### style

Vertical illustration in playing-card proportions (5:7). A precise natural-history-style drawing of a folded paper origami model: fine ink outlines, delicate cross-hatching, and meticulous colored-pencil shading. Every crease, fold edge, and overlapping layer of the paper is drawn crisply and accurately, as in a careful specimen plate. A subtle texture of off-white paper as the background.

### paper

The paper: a square sheet, white on the front side and red on the back side.

### model

A traditional Japanese origami crane (orizuru), with its long neck and pointed head, a straight tail, and both wings spread, seen slightly from the side and above. The white side faces out; red shows only where folds turn the back side outward.

### composition

The single finished model centered on the card, filling about two-thirds of its height. A quiet margin of off-white paper around it, especially above and below, so the image can be trimmed. A soft, faint shadow under the model. Even, soft light.

### constraints

The model must look like a real origami model folded from a single square sheet of paper, with no cuts and no glue. Paper is thin and flat, with sharp creases. No eyes, faces, or other drawn-on details on the paper. No hands, no other objects, no background scenery. No watercolor bleeding or blur, no glossy digital painting, no 3D rendering. No text, labels, numbers, card corner symbols, frames, borders, watermarks, or signatures.

## thumbnail

表と裏の画像ができたら、それぞれのサムネイルも作る。

- `card-front.png` から `card-front-thumb.png`、`card-back.png` から `card-back-thumb.png` を作る。
- 元の画像全体を縦横比を保って縮小し、背景色の余白を加えて正方形にする（幅 250px × 高さ 250px）。動物や折り紙を切り取らない。
