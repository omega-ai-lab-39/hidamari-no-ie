# ひだまりの家 ─ デザイン仕様書 (DESIGN.md)

リハビリデイサービス「ひだまりの家」（秋田県大仙市）コーポレートサイト。

---

## 1. コンセプト

> **「秋の陽だまりのような、あたたかい安心を。」**

高齢のご利用者が **迷わず・読みやすく** 使え、ご家族が **信頼** を寄せられるサイト。
将来の業務効率化ツール（利用者管理・リハビリ記録）を **同一デザイン言語** で拡張できる基盤を持つ。

### ターゲット
- **主**：ご利用者ご本人（70〜90代）／視力・可読性に最大配慮
- **副**：ご家族・ケアマネジャー（信頼・実績・安全性を判断）
- **将来**：スタッフ（業務ツール利用者）

---

## 2. 美学プロンプト（Claude Cookbook: Aesthetic 適用）

> Design with **restraint and warmth**. Use a **white, airy base** with generous
> whitespace so the content breathes. Choose a single **autumn-maple accent**
> (warm orange-red) used sparingly for emphasis and calls-to-action.
> Typography is **large and highly legible** — prioritize elderly readability
> over density. Rounded, soft edges; no harsh shadows; gentle motion only.
> Every element should feel **calm, trustworthy, and human**, never clinical.
> Accessibility (contrast, tap-target size, focus states) is a first-class
> requirement, not an afterthought.

**適用ルール**
- 装飾より **可読性**。1画面に要素を詰め込まない。
- アクセントは **1色**（もみじ色）に限定。多色化しない。
- アニメーションは **穏やか**（フェード/軽い浮き上がりのみ、300ms以内）。
- コントラスト比 **4.5:1 以上**、本文は **7:1** を目標。

---

## 3. カラーパレット（白ベース）

| 用途 | 変数 | 値 | 備考 |
|---|---|---|---|
| 背景（基調） | `--bg` | `#FFFFFF` | 純白ベース |
| 背景（面） | `--bg-soft` | `#FDF8F2` | ほのかな温白（セクション区切り） |
| 本文テキスト | `--text` | `#2E2A26` | 温かみのある濃グレー（純黒を避ける） |
| 補助テキスト | `--text-muted` | `#6B6259` | |
| アクセント（もみじ） | `--accent` | `#D9552B` | CTA・見出し強調 |
| アクセント濃 | `--accent-deep` | `#B23F1C` | hover |
| 若葉（副） | `--leaf` | `#7C9A5B` | 安心・自然の象徴、控えめに |
| 罫線 | `--line` | `#EDE4D8` | やわらかな境界 |

コントラスト：`--text` on `--bg` = 12:1、`--accent` on `#fff` = 4.6:1（AA適合）。

---

## 4. タイポグラフィ（文字大きめ）

- フォント：`"Noto Sans JP", system-ui, sans-serif`（丸みと視認性）
- **基準サイズ `18px`（一般より大きめ）**、行間 `1.9`

| 役割 | サイズ(clamp) | 太さ |
|---|---|---|
| Hero 見出し | `clamp(2.4rem, 6vw, 4rem)` | 700 |
| セクション見出し | `clamp(1.8rem, 4vw, 2.6rem)` | 700 |
| 小見出し | `1.35rem` | 600 |
| 本文 | `1.125rem`(=18px) | 400 |
| ボタン | `1.2rem` | 600 |

- 文字間隔 `0.02em`、和文の可読性優先。
- 高齢者配慮：本文最小 18px、タップ領域最小 **48×48px**。

---

## 5. レイアウト / コンポーネント

- 最大幅 `1080px`、左右パディング `clamp(1.25rem, 5vw, 3rem)`
- 角丸 `--radius: 18px`、影は `--shadow: 0 8px 30px rgba(180,120,80,.10)`（軽く温かい）
- ボタン：塗り（accent）／枠線（outline）の2種。大きめ・角丸。
- カード：白面＋やわらか影、hoverで2px浮上。

---

## 6. サイト構成（将来拡張を前提）

```
/                 … コーポレートサイト（本サイト）
  #hero           ヒーロー（キャッチ＋主要CTA）
  #about          ひだまりの家について
  #features       安心の3つの理由
  #services       リハビリ・サービス内容
  #flow           一日の過ごし方
  #price          ご利用案内・料金
  #access         アクセス・見学のご案内
  #contact        お問い合わせ
  footer          スタッフ専用ログイン導線（将来ツールへの入口）

/staff/  (将来)   … 業務効率化ツール（同デザイン言語で拡張）
  利用者管理 / リハビリ記録 / 実績レポート
```

**拡張設計の要点**
- CSS変数（デザイントークン）を `styles.css` に集約 → 業務ツールでも同ファイルを流用。
- フッターに「スタッフ専用」導線を予約配置（現状はプレースホルダ）。
- セクションはコンポーネント単位で独立 → 追加・差し替えが容易。

---

## 7. アクセシビリティ指針
- セマンティックHTML（`header/nav/main/section/footer`, 見出し階層）
- `:focus-visible` の明示、キーボード操作可
- 画像 `alt`、装飾要素は `aria-hidden`
- `prefers-reduced-motion` 尊重
- コントラスト AA 以上、本文 18px 以上
