# Evidence Reading Ledger / 根拠読解台帳

A bilingual format for keeping questions, claims, evidence, readings, and residual unknowns distinct.

問い、主張、根拠、読解、残余の未確定を混ぜずに残すための英日対応の記録形式です。

## Current release

Schemas and a fully synthetic example ledger are included in this repository. Source registries stay private until each item’s redistribution rights are verified.

ここにはスキーマと完全に合成した例を置いています。元の台帳は、各項目の再配布権を確認するまで非公開です。

## Included / 収録物

- `schemas/` — four append-only registry schemas
- `example/` — a fictional, cross-linked JSONL ledger; it contains no external evidence or personal data

## Read the example / 例を読む

Start with `example/CLAIM_REGISTRY.jsonl`, then follow its question and evidence IDs into the other files. The example intentionally keeps one question open.

`example/CLAIM_REGISTRY.jsonl` から読み始め、問いと根拠のIDを他のファイルへたどります。例では、ひとつの問いを意図的に未解決のまま残しています。

## Not a claim

An entry records a current reading; it does not make a claim permanently true.

台帳の記録はその時点の読解であり、主張を永久に真にするものではありません。
Bilingual schemas and examples for keeping questions, claims, evidence, and readings distinct.
