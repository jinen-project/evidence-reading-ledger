# SCHEMA — CLAIM_REGISTRY.jsonl

各トラックの主張の台帳。R は主張を作らず受け取る。append-only, 1 行 1 claim。

| field | type | 意味 |
|---|---|---|
| `id` | string | `C-####`。claim の一意 ID |
| `lens` | enum | **subject reading-lens**（意味名）: `Institution` / `Market` / `Human` / `Experience` / `Technology` / `Business`（拡張可）。R 内部の安定 lens で、canonical Dashboard の letter とは意図的に分離（対応表 = `ALIGNMENT_AUDIT.md`）。**owner-track ではない**（帰属は open owner decision・推定しない）。※旧 field 名 `track` は owner-track と誤読されるため `lens` に改称。**注**: これは主題の lens であり、`EVIDENCE_REGISTRY.lens`（CHI/psychology 等の venue/discipline 軸）とは別物。 |
| `source_repo` | string | 由来の repo/ファイル |
| `claim` | string | 主張の**原文（verbatim）**。AI の言い換えで上書きしない |
| `claim_normalized` | string | 接地可能な形に言い直した版（原文は保持したまま） |
| `status` | enum | **base grounding claim 用の Status Layer**（C-###/H-### 等）= Reading 群を評価した現在値: `asserted` / `candidate` / `supported` / `qualified` / `contested` / `refuted`。※design proposition(D-###)は `status` を使わず下記の二軸を使う。 |
| `verification_status` | enum | **根拠状態**（design proposition 用）: 一次資料の doc-fact が検証済か。`verified` / `partially-verified` / `unverified`。 |
| `adoption_status` | enum | **採用状態**（design proposition 用・別軸）: `supported-in-Japan` / `partially-supported` / `historically-supported` / `not-found` / `conflicted`。**doc-fact の真偽ではない**。 |
| `as_of` | string | status を最後に読んだ日付（`YYYY-MM-DD`）。**時間添字つき** |
| `question_ids` | string[] | QUESTION_REGISTRY の対応 id |
| `residual_unknown` | string | 現時点で世界に接続できていない部分 |
| `owner` | string | HA / track 担当 |
| `created` | string | `YYYY-MM-DD` |
| `supersedes` | string\|null | 旧行 id |

## status ladder（永続 grounded を持たない）

```
asserted → candidate → supported → qualified → contested → refuted
```

- `supported` = **現時点の evidence/reading で支持されている**状態。「真」ではない。
- `qualified` = 支持されるが条件付き（文化・文脈・サンプル依存など）。
- `contested` = 反する reading が併存。
- `refuted` = 覆された。
- **恒久的な `grounded` は使わない**。世界は更新される → 到達点は常に *Currently Grounded*（`as_of` 付き）。
- **status はパイプラインの段でなく、Reading の評価結果（Status Layer）**。Reading Pipeline(Question→Claim→Evidence→Reading)の外にある。
- status 更新は `supersedes` 付き新行で積む（旧 status は消さない・履歴を残す）。
- status 遷移の根拠は READING_MATRIX と REPORTS に残す。

## design proposition（D-###）と Japan-adoption 軸

海外学術の設計原則を日本行政へ移植可能か問う claim（`D-###`）は、以下の追加フィールドを持つ:
- `proposition_kind: "design proposition"` — **verified claim に昇格させない**印。`claim` は原則、`claim_normalized` は一次資料から直接言える doc-fact のみ。
- `reading_ids` — 対応する READING_MATRIX 行。
- `reopen_condition` — 一次未確認を解く人手確認等（Step の阻害条件ではない）。

**根拠状態と採用状態を分離する**（`status` 単一に潰さない）:
- `verification_status`（根拠）= 一次 doc-fact は `verified`。
- `adoption_status`（採用・別軸）= `supported-in-Japan` / `partially-supported` / `historically-supported`(current-status-unverified) / `not-found` / `conflicted`（6件を同一に揃えない）。
- **`partially-supported` を doc-fact の真偽状態にしない**。doc-fact は verified、採用は別。
規律: `academic support ≠ Japan adoption` / `historical statement ≠ current rule` / `similar practice ≠ same method` / `participation・co-creation ≠ co-production`。
- `claim` と `claim_normalized` を分ける（痕跡は解釈で上書きしない）。
