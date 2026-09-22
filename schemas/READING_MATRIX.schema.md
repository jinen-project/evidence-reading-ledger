# SCHEMA — READING_MATRIX.jsonl

**これは Evidence の台帳でなく Reading の台帳**。1 行 1 Reading。

> Matrix は `Claim × Evidence` ではなく **`Claim × Evidence → Reading`**。
> **セルそのものが Reading**。Evidence はセルの**外**にある（`evidence_id` で参照）。
> セルに入るのは supports/qualifies/contradicts という evidence の属性ではなく、**「私はこう読んだ」**（`reading`）と、その結果の `relation`。
> `relation` は Evidence の属性でなく **Reading の結果**。だから Evidence Matrix でなく Reading Matrix。
> Evidence は保存する（不変）。**Reading は更新する**（世界更新・新解釈で新しい行を足す）。

append-only, 1 行 1 reading。

| field | type | 意味 |
|---|---|---|
| `id` | string | `RD-####`。reading の一意 ID |
| `claim_id` | string | CLAIM_REGISTRY の `id` |
| `evidence_id` | string | EVIDENCE_REGISTRY の `id`（`verified` 必須） |
| `question_id` | string\|null | どの question に答える reading か |
| `relation` | enum | `supports` / `qualifies` / `contradicts` / `unknown`（＝Reading の判断） |
| `confidence` | enum | `high` / `medium` / `low`（Reading 自体の確からしさ） |
| `quote` | string | 原文の該当箇所（短く） |
| `locator` | string | 頁/節/図表/段落 |
| `reading` | string | **どう読んだか**の記述。evidence → relation を橋渡しする解釈 |
| `created` | string | `YYYY-MM-DD` |

## relation（Reading の判断）

- `supports` — この evidence を、claim を支持すると読んだ
- `qualifies` — 条件付き支持・限定と読んだ（文化/文脈/サンプル依存）
- `contradicts` — claim に反すると読んだ
- `unknown` — evidence は隣接領域だが**この点は答えていない**と読んだ（空欄でなく積極的に置く）

`unknown` の reading 群が、その claim の Residual Unknown の一次資料になる。
