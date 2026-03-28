# テレアポ分岐フロー ─ 強制実行ナビ v3

> **取りこぼしゼロ設計** ─ 一発で決めない、回収前提の営業構造

-----

## フロー全体図

```mermaid
flowchart TD
    LIST["1. リスト"]
    SCORE["2. スコアリング"]
    HYPOTHESIS["3. 仮説構築"]
    CALLGATE{"CALL判定\nスコア70以上?\n矛盾あり?\n直近トリガー?"}
    CALL["コール開始"]
    SKIP["スキップ\n条件未達"]
    FIRST["初回接触 10秒\n営業感を出すな"]
    FAIL10["10秒失敗\n営業感/違和感\n即終了"]
    JUDGE{"反応判定"}
    A["A: 食いつきあり\n売るな 広げろ"]
    B["B: 無関心\n追うな 即終了"]
    C["C: 仮説ズレ\n戦うな 即撤退"]
    ANEXT{"Aの次の動き"}
    A_DETAIL["相手に言わせる\nどうしたいですか?\n何があれば判断できる?"]
    A_HOLD["保留\n期限切って再連絡"]
    LOG["ログ記録\n1.刺さった仮説\n2.反応ABC\n3.業種"]
    RECALLGATE{"再コール判定\nA_HOLD?\nB+違和感?"}
    RECALL["再コール\n3日以内\n仮説修正"]
    CLOSE["完了\nリスト戻し"]
    NG["NG: 説明/売込み/粘り"]

    LIST --> SCORE --> HYPOTHESIS --> CALLGATE
    CALLGATE -- "トリガーあり" --> CALL
    CALLGATE -- "条件未達" --> SKIP
    SKIP -. "次のリストへ" .-> LIST
    CALL --> FIRST
    FIRST -- "OK突破" --> JUDGE
    FIRST -- "失敗" --> FAIL10
    FAIL10 --> LOG
    JUDGE -- "反応あり" --> A
    JUDGE -- "無反応" --> B
    JUDGE -- "否定" --> C
    A --> ANEXT
    ANEXT -- "相手が動いた" --> A_DETAIL
    ANEXT -- "迷い中" --> A_HOLD
    A_DETAIL --> LOG
    A_HOLD --> LOG
    B --> LOG
    C --> LOG
    LOG --> RECALLGATE
    RECALLGATE -- "回収対象あり" --> RECALL
    RECALLGATE -- "対象外" --> CLOSE
    RECALL -- "3日以内" --> FIRST
    CLOSE -. "次のリストへ" .-> LIST
    NG -.- FIRST
    NG -.- A
    NG -.- B
    NG -.- C

    style LIST fill:#0d2744,stroke:#448aff,color:#448aff
    style SCORE fill:#0d2744,stroke:#448aff,color:#448aff
    style HYPOTHESIS fill:#0d2744,stroke:#448aff,color:#448aff
    style CALL fill:#0d2744,stroke:#448aff,color:#448aff
    style FIRST fill:#0d2744,stroke:#448aff,color:#fff
    style CALLGATE fill:#3e2e00,stroke:#ffd600,color:#ffd600
    style SKIP fill:#16213e,stroke:#546e7a,color:#cfd8dc
    style FAIL10 fill:#4a0e0e,stroke:#ff5252,color:#ff8a80
    style JUDGE fill:#16213e,stroke:#90a4ae,color:#fff
    style A fill:#1b5e20,stroke:#00e676,color:#00e676
    style B fill:#4a0e0e,stroke:#ff1744,color:#ff1744
    style C fill:#3e2e00,stroke:#ffd600,color:#ffd600
    style ANEXT fill:#1b5e20,stroke:#00e676,color:#00e676
    style A_DETAIL fill:#1b5e20,stroke:#00e676,color:#00e676
    style A_HOLD fill:#3e2e00,stroke:#ffd600,color:#ffd600
    style LOG fill:#16213e,stroke:#546e7a,color:#cfd8dc
    style RECALLGATE fill:#1a237e,stroke:#82b1ff,color:#82b1ff
    style RECALL fill:#1a237e,stroke:#82b1ff,color:#82b1ff
    style CLOSE fill:#16213e,stroke:#546e7a,color:#cfd8dc
    style NG fill:#3a0a0a,stroke:#ff1744,color:#ff8a80
```

-----

## 各ノード詳細

### CALL判定（コール前ゲート）

|条件      |内容                       |
|--------|-------------------------|
|スコア70以上 |リストスコアリング基準              |
|矛盾あり    |外部情報と実態のギャップ             |
|直近トリガーあり|採用 / SNS投稿 / レビュー増 / 組織変更|


> 条件未達 → スキップ → 次のリストへ

### 初回接触（10秒ルール）

|項目  |内容                    |
|----|----------------------|
|判断  |**営業感を出すな**           |
|一言目 |「営業じゃなくて一点だけ確認です」     |
|一言目 |「〇〇ですよね？」             |
|失敗条件|営業感が出た / 違和感を与えた → 即終了|

### A：食いつきあり

|項目      |内容                        |
|--------|--------------------------|
|判断      |**売るな、広げろ**               |
|セリフ     |「今どうされてます？」               |
|セリフ     |「取りこぼしてますよね？」             |
|セリフ     |「事例1つだけ共有します」             |
|相手が動いた →|「どうしたいですか？」「何があれば判断できますか？」|
|迷い中 →   |保留（期限切って再連絡）              |

### B：無関心

|項目 |内容                 |
|---|-------------------|
|判断 |**追うな**            |
|セリフ|「失礼しました、またタイミング見ます」|
|結果 |即終了                |

### C：否定 / 仮説ズレ

|項目 |内容              |
|---|----------------|
|判断 |**戦うな**         |
|セリフ|「失礼しました、認識違いでした」|
|結果 |即撤退             |

### 再コール判定

|対象    |条件                   |
|------|---------------------|
|A_HOLD|保留案件                 |
|B＋違和感 |無関心だが引っかかりあり         |
|期限    |**3日以内に実行**          |
|方法    |仮説を修正して再アプローチ → 初回接触へ|

-----

## NG行為（全フェーズ共通）

- 説明し始める
- 売り込む
- 粘る

> **これやったら負け確定**

-----

## ログ記録（3項目だけ）

1. 刺さった仮説
1. 反応タイプ（A / B / C）
1. 業種

> これ以上書くな ─ 3つで十分

-----

*考えるな、従え。*
