---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable Comark Syntax: https://comark.dev/syntax/markdown
comark: true
# duration of the presentation
duration: 35min
# fonts loaded from Google Fonts
fonts:
  sans: PT Serif
  provider: google
---

# Game Development with Unity AI

---
layout: two-cols
---

# Generators

- アセット生成機能
  - 画像生成（スプライト、テクスチャ、キューブマップ、マテリアル）
  - スプライトアニメーション生成（動画→スプライトシート）
  - 3D モデル生成
  - キャラクターアニメーション生成
  - サウンド生成（効果音、台詞、音楽）

::right::

<img src="/img/Title_Heroes.png" alt="Title Heroes" />

<style>
.two-columns { grid-template-columns: 3fr 1fr; }
.two-columns .col-right { display: flex; flex-direction: column; justify-content: flex-end; }
</style>

<!--
最後に Generator という、アセット生成機能のコレクションが存在します。ここでは様々なサードパーティの生成モデルを使用して、各種のアセットを生成することができます。

この画像のように Generator ウィンドウを使って自分でプロンプトを打ち込んで生成することができます。また、AI Assistant もこの Generator を使用する能力を持っているので、生成を AI Assistant に任せて自動化することも可能です。
-->
