# SCHEMA — EVIDENCE_REGISTRY.jsonl

**Evidence object** の台帳（旧 KNOWLEDGE_REGISTRY を改名）。

> なぜ Knowledge でないか: Paper / Law / Dataset / Observation / Interview / Experiment は、それ自体は **Knowledge ではなく Evidence Object**。
> Knowledge になるのは、その Evidence を **Reading** で読んだ後（READING_MATRIX → Grounding）。だから生の対象はここに Evidence として置く。

append-only, 1 行 1 evidence object。

| field | type | 意味 |
|---|---|---|
| `id` | string | `EV-####`。evidence object の一意 ID |
| `type` | enum | `Paper` / `Book` / `Spec` / `Law` / `Standard` / `Dataset` / `Interview` / `Observation` / `Experiment` |
| `title` | string | 表題 |
| `authors` | string | 著者/発行体 |
| `year` | number\|null | 発行年 |
| `venue` | string | 掲載先（journal/conference/発行元） |
| `lens` | enum | 9レンズ: `CHI`/`DIS`/`UIST`/`CSCW`/`IJHCS`/`cogsci`/`psychology`/`UX`/`public_admin`/`other` |
| `identifier` | string | DOI / ISBN / URL / 法令番号 / データセット ID |
| `verification` | enum | `verified` / `unverified` / `secondary`（METHOD §3） |
| `verified_via` | string | 検証手段 |
| `note` | string | 一言メモ（サンプル/手法/対象） |
| `created` | string | `YYYY-MM-DD` |

**任意フィールド（domain 別に付与）**:
- `domain` — Session 別の主題ドメイン（例: HCI/Trust/Decision/JapanAdmin…）。9レンズ(`lens`)とは別軸。
- `norm_strength` — 規範強度（法律 / 標準 / ガイド / 参考）。行政一次資料で分離が要るとき。
- `currency` — 現行性（現行 / 期間満了 / 継承 / 廃止）。規範強度と**分離して**記録する。

- `verification=verified` の evidence のみ READING_MATRIX で `supports/contradicts` に使える。
- `unverified` は引用不可。`secondary` は `qualifies` 止まり。
- **Knowledge はここに置かない**。Knowledge は Reading を統合した後、Grounding／REPORTS に生成される下流物。
