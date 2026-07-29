---
title: "Dataset bước 3: Local preview và split"
date: 2026-07-29
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

Chạy cùng logic preprocessing trước khi tạo AWS job:

```powershell
python preprocessing/processing_script.py `
  --input data_generation/sample_trajectories.jsonl `
  --output-dir data/processed
```

Kỳ vọng output `Train=840, Val=180, Test=180`. Kiểm tra distribution bằng Python standard library:

```powershell
@'
import csv
from collections import Counter
for name in ('train', 'validation', 'test'):
    with open(f'data/processed/{name}.csv', newline='', encoding='utf-8') as f:
        rows = list(csv.DictReader(f))
    print(name, len(rows), dict(sorted(Counter(r['label'] for r in rows).items())))
'@ | python -
```

`train_test_split(..., stratify=df["label"], random_state=42)` giữ tỷ lệ class gần nhau giữa các split.

> **[ẢNH PLACEHOLDER — local processed data]** Chụp command output có 840/180/180 và distribution 6 labels. Đây là evidence local, không thay thế AWS Processing evidence.

