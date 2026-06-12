# /trump-event — トランプ種目エントリー生成スキル

引数として渡された種目名（例: `/trump-event ブラックジャック`）に基づき、
以下の **2つの成果物** を生成する。

1. `data/details/{id}.html` として保存する **HTMLファイル**
2. `data/events.json` の `events` 配列に追加する **JSONオブジェクト**（`detail: ""`）

## ファイル保存の流れ

```
/trump-event ブラックジャック
  → HTMLを生成 → data/details/blackjack.html として Write ツールで保存
  → JSONオブジェクトを出力 → events.json の events 配列末尾に追加
```

## 生成手順

1. 以下の **HTMLテンプレート** を種目の内容で埋めた自己完結型HTMLを作成する
2. `data/details/{id}.html` として保存する
3. **JSONオブジェクト**（`detail: ""`）を出力し、events.json への追加方法を示す

---

## HTMLテンプレート（6セクション必須）

```html
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<style>
  body { font-family: "Helvetica Neue", sans-serif; padding: 1rem 1.5rem; color: #222; line-height: 1.75; max-width: 720px; margin: 0 auto; }
  h1   { color: #DC2626; border-bottom: 3px solid #DC2626; padding-bottom: .4rem; font-size: 1.6rem; }
  h2   { color: #B91C1C; margin-top: 1.8rem; font-size: 1.1rem; display: flex; align-items: center; gap: .4rem; }
  ul, ol { padding-left: 1.4rem; }
  li   { margin-bottom: .35rem; }
  .meta { background: #fff5f5; border-left: 4px solid #DC2626; border-radius: 0 8px 8px 0; padding: .8rem 1.2rem; margin: 1rem 0; }
  .meta p { margin: 0; }
  table { border-collapse: collapse; width: 100%; margin-top: .5rem; }
  th, td { border: 1px solid #fecaca; padding: .4rem .7rem; text-align: left; font-size: .92rem; }
  th { background: #fee2e2; }
</style>
</head>
<body>

<h1>🃏 {種目名}</h1>

<section>
  <h2>📋 概要</h2>
  <p>{ゲームの概要・特徴・プレイ感を2〜3文で説明}</p>
</section>

<section>
  <h2>🎯 ゲームの目的</h2>
  <p>{勝利条件・ゲームの目標を1〜2文で説明}</p>
</section>

<section>
  <h2>🃏 基本ルール</h2>
  <ul>
    <li>{基本ルール1}</li>
    <li>{基本ルール2}</li>
    <li>{基本ルール3 …}</li>
  </ul>
</section>

<section>
  <h2>🎉 楽しみ方</h2>
  <ul>
    <li>{教会グループでの楽しみ方・アレンジ例1}</li>
    <li>{楽しみ方2}</li>
    <li>{楽しみ方3 …}</li>
  </ul>
</section>

<section class="meta">
  <h2>👥 プレイ人数</h2>
  <p>{最小人数}〜{最大人数}人（推奨: {推奨人数}人）</p>
</section>

<section>
  <h2>🛒 必要なもの</h2>
  <table>
    <tr><th>アイテム</th><th>数量・備考</th></tr>
    <tr><td>{アイテム名}</td><td>{数量・備考}</td></tr>
    <tr><td>{追加アイテム（あれば）}</td><td>{備考}</td></tr>
  </table>
</section>

</body>
</html>
```

---

## JSONオブジェクトテンプレート

`detail` は空文字のまま。HTMLは `data/details/{id}.html` に保存する。

```json
{
  "id": "{kebab-case-id}",
  "category": "trump",
  "title": "{種目名（日本語）}",
  "summary": "{1〜2行の概要}",
  "peopleMin": 0,
  "peopleMax": 0,
  "seasons": ["通年"],
  "budget": "free",
  "tags": ["屋内", "カードゲーム"],
  "detailFormat": "html",
  "detail": "",
  "history": [],
  "createdAt": "2026-06-12",
  "updatedAt": "2026-06-12"
}
```

---

## フィールド記入ガイドライン

| フィールド | 値の基準 |
|-----------|---------|
| `id` | 種目名の英語kebab-case（例: `blackjack`, `texas-holdem`） |
| `budget` | トランプ持参なら`free` / 新規購入が必要なら`low`（1組300〜500円） |
| `seasons` | 屋内トランプは基本`["通年"]` |
| `peopleMin` | ゲーム成立の最低人数 |
| `peopleMax` | ゲームの現実的な上限（無制限なら20） |
| `tags` | 屋内/対戦/協力/チーム戦/個人戦/推理/心理戦/記憶/運/戦略/初心者向け/子ども向け/大人向け/トリックテイキング/競技向け/ギャンブル要素なし など |
