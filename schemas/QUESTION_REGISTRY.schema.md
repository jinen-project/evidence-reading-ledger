# SCHEMA — QUESTION_REGISTRY.jsonl

起点の台帳。1 claim を反証可能な問いに変換して積む。append-only, 1 行 1 question。

| field | type | 意味 |
|---|---|---|
| `id` | string | `Q-####`。question の一意 ID |
| `claim_id` | string | 対応する CLAIM_REGISTRY の `id` |
| `kind` | enum | `definition` / `falsification` / `discrimination` / `external_validity` / `reach` |
| `question` | string | 反証可能な問い（測定・データに落ちる形） |
| `answerable_by` | string[] | どんな knowledge type/venue なら答えうるか（例: `["Paper:psychology","Dataset"]`） |
| `status` | enum | `open` / `partially_answered` / `answered` / `unanswerable` |
| `answer_summary` | string | 現時点の到達（空可）。原文は READING_MATRIX/REPORTS を参照 |
| `feeds_residual` | bool | この問いが Residual Unknown に流れているか |
| `created` | string | `YYYY-MM-DD` |
| `supersedes` | string\|null | 旧行 id（更新時） |

`kind` は METHOD §2 の5分類に対応。`reach` は必ず Residual Unknown に接続する。
