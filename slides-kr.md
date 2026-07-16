---
theme: seriph
title: Unity AI Examples
colorSchema: dark
layout: default

drawings:
  persist: false
  syncAll: false

transition: slide-left

comark: true

duration: 40min

fonts:
  sans: Inter
  provider: google
---

<div class="h-full flex flex-col items-center justify-center text-center gap-10" style="color:#ff4444">
  <div class="text-3xl font-extrabold" style="line-height:1.5">
    This session will be presented from<br>the speaker's laptop using a custom presentation app.
  </div>
  <div class="text-3xl font-extrabold" style="line-height:1.5">
    This PPTX file is for review purposes only.<br>It does not contain any videos or audio.
  </div>
</div>

---
layout: cover
class: text-center
---

# Developing with Unity AI:<br>Practical Use Cases

<!--
みなさんこんにちは。Unity Technologies Japan の高橋啓治郎と申します。

このセッションでは Unity AI を実際のプロジェクトで使用した体験についてお話しします。僕は Unity AI を実際に幾つかのゲームプロジェクトや技術デモの制作に使用しました。そこで Unity AI が実際のプロジェクト開発においてどのように使えるのか、ということについて、様々な知見を得ることができました。今日はそれらの知見について皆さんと共有したいと思います。
-->

---
layout: section
---

# Introducing the Projects

<!--
それではまず始めに、実際に Unity AI を使用して開発したプロジェクトを、順番に紹介していきます。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover" print-timestamp="3" print-poster="/mm-pr-hq-print.jpg">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Mirror Mage

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3" print-poster="/mm-pr-hq-print.jpg">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
まず最初のこのプロジェクトは "Mirror Mage" というカジュアルゲームです。敵の攻撃を反射して、それを攻撃に使う、というちょっと変わったシステムのアクションゲームです。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover" print-timestamp="3" print-poster="/mh-pr-hq-print.jpg">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Dungeon Match Heroes

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3" print-poster="/mh-pr-hq-print.jpg">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
次のプロジェクトは "Dungeon Match Heroes" というカジュアルゲームです。マッチ３パズルゲームに RPG のエッセンスを加えたようなゲームですね。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover" print-timestamp="3" print-poster="/dm-pr-hq-print.jpg">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Drift Mayhem

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3" print-poster="/dm-pr-hq-print.jpg">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
３つ目は "Drift Mayhem" という、ドライブゲームとシューティングゲームが融合したようなタイプのゲームですね。
-->

---

<div class="h-full flex flex-col">

# Mesh Slicer

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3" print-poster="/ms-demo-hq-print.jpg">
  <source src="/ms-demo-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
そして最後に、これはゲームではなく技術デモですが、Mesh Slicer というプロジェクトです。3D モデルをマウスで切断する処理を開発して、それのインタラクティブデモを作成しました。
-->

---
layout: section
---

# Categorizing Development Approaches

<!--
さて、これらのプロジェクトの解説に入る前に、AI エージェントを使った開発アプローチの分類について触れたいと思います。

というのも、AI エージェントをゲーム開発に使用するにあたっては、そのエージェントの使い方・動かし方について、いくつかの異なるアプローチが存在すると考えています。
-->

---

<div class="h-full flex flex-col">

<div class="flex-1 min-h-0 flex items-center justify-center gap-16">

<div class="flex flex-col items-center justify-center gap-8">
  <div class="text-xl">Interactive</div>
  <svg width="260" height="220" viewBox="0 0 260 220" fill="none" stroke="currentColor" stroke-width="2">
    <defs>
      <marker id="ahA" viewBox="0 0 10 10" markerWidth="6" markerHeight="6" refX="9" refY="5" orient="auto">
        <path d="M0 0 L10 5 L0 10 Z" fill="currentColor" stroke="none" />
      </marker>
    </defs>
    <text x="45" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🧑</text>
    <text x="215" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🤖</text>
    <path d="M45 70 V55 Q45 45 55 45 H205 Q215 45 215 55 V70" marker-end="url(#ahA)" stroke-linecap="round" stroke-linejoin="round" />
    <path d="M215 146 V160 Q215 170 205 170 H55 Q45 170 45 160 V146" marker-end="url(#ahA)" stroke-linecap="round" stroke-linejoin="round" />
    <text x="130" y="18" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">💬</text>
    <text x="130" y="197" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">💬</text>
  </svg>
</div>

<div class="w-px self-center h-48 bg-gray-400 opacity-30"></div>

<div class="flex flex-col items-center justify-center gap-8">
  <div class="text-xl">Autonomous</div>
  <svg width="330" height="190" viewBox="0 0 330 190" fill="none" stroke="currentColor" stroke-width="2">
    <defs>
      <marker id="ahB" viewBox="0 0 10 10" markerWidth="6" markerHeight="6" refX="9" refY="5" orient="auto">
        <path d="M0 0 L10 5 L0 10 Z" fill="currentColor" stroke="none" />
      </marker>
    </defs>
    <text x="35" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🧑</text>
    <text x="195" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🤖</text>
    <path d="M73 108 H157" marker-end="url(#ahB)" stroke-linecap="round" />
    <path d="M195 146 V161 Q195 171 205 171 H265 Q275 171 275 161 V38 Q275 28 265 28 H205 Q195 28 195 38 V70" marker-end="url(#ahB)" stroke-linecap="round" stroke-linejoin="round" />
    <text x="115" y="76" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">📄</text>
    <text x="300" y="100" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">⚙️</text>
  </svg>
</div>

</div>

</div>

<!--

１つは AI エージェントとの対話的な開発アプローチ、もう１つは、AI エージェントを独立して長時間実行させる自律的な開発アプローチです。

前者は人間の手が介在することを前提とした、いわゆる human-in-the-loop なスタイルですね。それに対して後者は、人間の手が介在する要素を極力排除して、なるべく AI エージェントが止まることなく動き続けることを目標にします。

昨今は自律的実行性能の高いフロンティアモデルを使用して、この自律的なアプローチでどれだけ効率的に開発を進めるか、というのが注目を集めていますよね。

ですが、ここは意見の分かれるところになると思いますが、実際のゲーム開発においては対話的な要素を完全に無くすことは難しいと思います。

これは皆さん直感的に分かることだと思いますが、ゲームの評価は人間の感覚に頼る部分が多くあります。実際に見たり触ったりしないと良いか悪いかわからない、という部分ですね。

またそういった感覚的な要素だけでなく、例えばユーザの反応はどうなるだろうか、とか、過去の作品とどう連続性を持つか、とか、現時点の文化においてどういった意味を持ちうるか、とか、自分たちのビジネスとどう接続されるのか、とか、そういった社会的な文脈を持って判断を行なっていくことは、非常に難しいことです。そこから人の手と頭脳を排除していくほどに、その判断能力は希薄化していく気がしています。

ただその反面、そういった判断が必要とされないタスクも、ゲーム開発には数多く存在します。例えば、効率的なデータ構造を設計して、それに関するツールを揃えて欲しい、とか、特定の用途に合わせた効率的なシーケンス制御を組んで欲しいとか、そういった類のものですね。
-->

---

<div class="h-full flex flex-col justify-center px-10">
<div class="grid items-center gap-x-6 gap-y-4" style="grid-template-columns: auto 1fr auto;">
<div class="flex justify-center">
<div class="relative" style="width:206px;height:136px">
<img src="/mm-pr-hq-thumb.png" class="absolute w-40 rounded shadow" style="top:0;left:0" />
<img src="/mh-pr-hq-thumb.png" class="absolute w-40 rounded shadow" style="top:22px;left:22px" />
<img src="/dm-pr-hq-thumb.png" class="absolute w-40 rounded shadow" style="top:44px;left:44px" />
</div>
</div>
<div class="flex flex-col items-center gap-1">
<svg width="164" height="120" viewBox="0 0 260 190" fill="none" stroke="currentColor" stroke-width="3">
<defs><marker id="tA" viewBox="0 0 10 10" markerWidth="6" markerHeight="6" refX="9" refY="5" orient="auto"><path d="M0 0 L10 5 L0 10 Z" fill="currentColor" stroke="none" /></marker></defs>
<text x="45" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🧑</text>
<text x="215" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🤖</text>
<path d="M45 70 V55 Q45 45 55 45 H205 Q215 45 215 55 V70" marker-end="url(#tA)" stroke-linecap="round" stroke-linejoin="round" />
<path d="M215 146 V160 Q215 170 205 170 H55 Q45 170 45 160 V146" marker-end="url(#tA)" stroke-linecap="round" stroke-linejoin="round" />
</svg>
<div class="text-lg font-bold">Interactive</div>
</div>
<div class="text-lg text-center">Workhorse / lightweight models</div>
<div style="grid-column:1/-1" class="border-t border-gray-300"></div>
<div class="flex justify-center">
<img src="/ms-demo-hq-thumb.png" class="w-40 rounded shadow" />
</div>
<div class="flex flex-col items-center gap-1">
<svg width="189" height="120" viewBox="0 0 300 190" fill="none" stroke="currentColor" stroke-width="3">
<defs><marker id="tB" viewBox="0 0 10 10" markerWidth="6" markerHeight="6" refX="9" refY="5" orient="auto"><path d="M0 0 L10 5 L0 10 Z" fill="currentColor" stroke="none" /></marker></defs>
<text x="35" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🧑</text>
<text x="195" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🤖</text>
<path d="M73 108 H157" marker-end="url(#tB)" stroke-linecap="round" />
<path d="M195 146 V161 Q195 171 205 171 H265 Q275 171 275 161 V38 Q275 28 265 28 H205 Q195 28 195 38 V70" marker-end="url(#tB)" stroke-linecap="round" stroke-linejoin="round" />
</svg>
<div class="text-lg font-bold">Autonomous</div>
</div>
<div class="text-lg text-center">Frontier models</div>
</div>
</div>

<!--
僕のプロジェクトでも 3D モデルのメッシュを切断するという処理には、文化的な判断や社会的な要素も存在しませんので、このカテゴリに属することになります。ここでは、人間の手を介在させない、自律的なアプローチが有効になり得ます。ここでは Opus 4.8 のようなフロンティアモデルを使用しました。

それ以外のゲームプロジェクトについては、対話的な開発アプローチをとりました。そして、対話を効率良く、つまりレスポンス良く低コストに進めるために、比較的軽量なモデル、Unity Lite や Unity Default を使用しました。

このような分類と、それによるツールやモデルの選択は、これらのプロジェクトにおいて意識的に行なっていくことになりますので、まず最初にここで整理しておきました。
-->

---
layout: chapter
---

<BgVideo src="/mm-pr-hq.mp4" />

# Project: Mirror Mage

<!--
さて、ここからは、先ほど紹介した４つのプロジェクトを順番に掘り下げていきたいと思います。最初のプロジェクトは Mirror Mage です。
-->

---
layout: two-cols-video
---

# Game Overview

- A "survivors-like" game starring a mage who can only use defensive magic.
- Reflect enemy bullets with your barrier and hit enemies with them to defeat them.
- Gain experience to level up. You can choose abilities to grow.

::right::

<SlidevVideo muted autoplay loop print-timestamp="3" print-poster="/mm-pr-hq-print.jpg">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このゲームは、防御魔法しか使えない魔法使いを主人公とした、いわゆる "Survivors" 系のアクションゲームです。敵の攻撃を、この魔法陣バリアで跳ね返すことができます。跳ね返した弾にはコリジョンがあって、これを敵に当てることで、敵を倒せます。

主人公は経験値を貯めることでレベルアップします。その際にスキルを選択してパワーアップさせることができます。例えば、移動速度を速くしたり、バリアの大きさを大きくしたり、というようなことですね。
-->

---
layout: image-right
image: /mm-bg.png
---

# Development Background

- My first Unity AI showcase project
- Used Unity Lite
- Generated almost all assets
- Used AI Assistant for Editor operations too
- Built in about 10 days

<!--
このプロジェクトの開発背景を少し話しておきたいと思います。これは個人的に初めて作った Unity AI のプロジェクトでした。当時はまだ Unity Lite モデルしか存在していなかったので、すべての作業を Unity Lite で行なっています。

プロジェクト内で使用しているアセットは基本的にすべて Unity AI で生成しています。C# スクリプトやシェーダーは AI Assistant で作成していますし、スプライトや、アニメーション、効果音などもすべて Unity AI の Generator で作成しました。

また、AI Assistant にどこまで作業を任せられるか知りたかったので、Unity Editor の操作もほとんど AI Assistant に任せるようにしました。結果的に、自分の手で Hierarchy や Scene View を操作することは殆どありませんでした。

このプロジェクトは色々と実験しながら作業を行って、約１０日間でこのような形になりました。
-->

---
layout: section
---

# Development Process

<!--
次にこのプロジェクトの開発の流れについて解説していきますが、これは最初のプロジェクトなので、本当に概要だけサラッと流していきましょう。
-->

---

<div class="h-full flex flex-col">

# The First Prototype

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="10" print-poster="/mm-reflex-shooter-print.jpg">
  <source src="/mm-reflex-shooter.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
まず最初に作成したプロトタイプは、こんな感じでした。全然違うゲームだったのが分かると思います。「敵の弾を反射して利用する」というコアのメカニクスは同じなのですが、最初は SF 風のテーマの 2D シューティングゲームとして作っていました。
-->

---

# Prototype Prompt

<blockquote>
다음과 같은 2D 슈팅 게임을 만들어 주세요.

- 플레이어 기체는 마우스 커서를 일정 속도 이하로 부드럽게 따라간다.
- 적은 화면 바깥 둘레에서 등장해 플레이어 기체에게 다가온다.
- 적은 상당한 밀도로 탄을 쏘지만, 플레이어 기체를 완전히 조준하는 것이 아니라 어느 정도 흩어지게 쏜다.
- 플레이어 기체는 탄에 충돌하면 폭발한다.
  - 폭발 후 일정 시간이 지나면 게임을 처음부터 다시 시작한다.
- 플레이어 기체는 마우스 버튼을 누르고 있는 동안 반사 배리어를 전개한다.
- 반사 배리어를 전개하는 동안 플레이어 기체의 에너지는 계속 줄어든다.
- 플레이어 기체의 에너지는 반사 배리어를 해제한 뒤 기체를 정지시키면 서서히 회복된다.
- 반사 배리어에 맞은 적탄은 튕겨 나간다. 이때 적탄의 속도는 두 배가 된다.
- 튕겨 나간 적탄은 적에 대한 충돌 판정을 가지며, 적을 파괴할 수 있다.
- 아트 스타일은 Sci-Fi를 기본 테마로 한다.

</blockquote>

<!--
このプロトタイプは、こんな感じのプロンプトで、ほぼ one shot で作成しました。Unity Lite のような軽量モデルでも、この程度のタスクなら難なくこなせますね。
-->

---

<div class="h-full flex flex-col">

# Change of Direction

- It showed little room to grow as a shooter, and I couldn't see how to develop it further.
- So I made a bold move and rebuilt it as a "survivors-like" game.

<img src="/mm-design-change.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
ただ、このプロトタイプを実際に作ってみて感じたのですが、シューティングゲームとしての伸び代が感じられなくて、この後どう発展させていくべきか分からなくなってきました。

そこで、大幅な方針転換を行うことにしました。古典的なシューティングゲームではなく、いわゆる "Survivors" 系のゲームとして作り替えてみよう、と考えたわけです。

この方針転換によって大きく道がひらけました。顔の無い宇宙船ではなく、分かりやすく人格の見えるキャラクターになって、またそこから、防御しかできないことの物語的必然性が生まれました。また、パワーアップ要素は RPG 的な成長要素として解釈できるようになりました。

このような大きな方針転換は、従来であれば精神的負荷の高い大変な作業であったと思いますが、AI assisted なゲーム開発であれば、その負荷はだいぶ軽くなります。特に今回のように初期プロトタイプの段階であれば、容易に転換が可能です。

こうして、素早くプロトタイピングを行いながら、人間の手によって評価を行い、人間のアイデアによって改良を重ね、自分たちの求める内容へと近付けていく、というアプローチが可能なのだなと、このプロジェクトで実感することができました。
-->

---

<div class="h-full flex flex-col">

# Retro-Game-Style Effect

- Used the "KinoEight" effect I developed in the past

<img src="/mm-filter-comparison.png" class="flex-1 min-h-0 w-full object-contain mt-4" style="image-rendering: pixelated;" />

</div>

<!--
次に、このプロジェクトで使用したレトロゲーム風エフェクトについて触れておきたいと思います。

このプロジェクトでは、過去に僕が開発した "KinoEight" エフェクトを使って、このレトロゲーム風の見た目を作り出しています。この左側の画像がエフェクト無しの状態のもので、右側の画像がエフェクトを適用した状態のものです。使用する色の数や解像度を落とした上でディザリングをかけることで、この見た目を作り出しています。
-->

---

<div class="h-full flex flex-col">

# Why I Added the Effect

- It wasn't simply about getting a retro look.
- The goal was to equalize the "information density" of the assets.
- Uneven density makes the visuals feel disjointed.

<img src="/mm-style-comparison.png" class="flex-1 min-h-0 w-full object-contain mt-4" style="image-rendering: pixelated;" />

</div>

<!--
このエフェクトを入れた理由ですが、実は、レトロゲーム風の見た目にしたかったわけではありません。他の理由があります。それは「アセットの持つ情報密度の均一化」です。

これは個人的な考え方になるのですが、スプライトなどの画像アセットの見た目を印象付ける要素の一つとして、「情報量の密度」というものがあると考えています。それは例えば、絵としての描き込みの細かさや、色彩の深さなどを表しています。

そして、この情報密度がバラバラだと、それらのアセットを統合している感覚が薄れてしまいます。何か寄せ集めを切り貼りしたような雰囲気になってしまうんですよね。

例えば、この主人公と敵キャラクターのスプライト、背景の画像を並べてみると、一応似せる努力はしているんですが、それでも書き込みの密度や色彩の使い方にかなりバラつきがが出ていると感じました。
-->

---

<div class="h-full flex flex-col">

# Equalizing Information Density

<div class="flex-1 min-h-0 flex flex-col items-center justify-center gap-6">

<div class="flex flex-col items-center gap-2">
  <div class="flex gap-4 items-center">
    <DensityTile :n="11" :palette="['#c0392b', '#27ae60', '#39AAFF', '#8e44ad', '#f39c12', '#16a085', '#e67e22', '#2c3e50']" />
    <DensityTile :n="8" :palette="['#e74c3c', '#3498db', '#f1c40f', '#9b59b6', '#1abc9c', '#e67e22']" />
    <DensityTile :n="6" :palette="['#39AAFF', '#e67e22']" :seed="42" />
  </div>
</div>

<div class="relative flex items-center justify-center h-26 opacity-70">
  <svg width="28" height="104" viewBox="0 0 28 104">
    <line x1="14" y1="2" x2="14" y2="95" stroke="currentColor" stroke-width="2" />
    <path d="M9 93 L14 102 L19 93 Z" fill="currentColor" stroke="none" />
  </svg>
  <div class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 px-4 py-1 text-sm border rounded bg-black" style="border-color: currentColor;">filtering</div>
</div>

<div class="flex flex-col items-center gap-2">
  <div class="flex gap-4 items-center">
    <DensityTile :n="6" :palette="['#39AAFF', '#e67e22']" />
    <DensityTile :n="6" :palette="['#39AAFF', '#e67e22']" />
    <DensityTile :n="6" :palette="['#39AAFF', '#e67e22']" :seed="42" />
  </div>
</div>

</div>

</div>

<!--
これを強制的に均一化する方法として、「一旦すべてのアセットの情報量を削って落とす」というものがあります。密度の低い方に合わせることによって、統合された感じを生み出そうというわけですね。

今回使用した KinoEight エフェクトは、解像度と色彩を強制的に落とすことによって、そのような効果を生み出すことができると考えています。

ただしこれは、品質を劣化させることで見た目を揃える、ということなので、実はあまり使いたくないテクニックです。今回は Unity AI を使うのが初めてだったので、安直なテクニックに頼ってみた、という感じです。
-->

---
layout: chapter
---

<BgVideo src="/mh-pr-hq.mp4" />

# Project: Dungeon Match Heroes

<!--
さて、最初のプロジェクトの解説はこのぐらいにして、次は２つ目に取り組んだプロジェクト、Dungeon Match Heroes について解説したいと思います。
-->

---
layout: two-cols-video
---

# Game Overview

- A fusion of match-3 puzzle and RPG.
- Only blocks in the bottom row of the grid can be broken by clicking.
- Matching blocks triggers the effect each block carries.
  - Sword block = attack, potion block = heal, etc.
- Gain experience to level up.
  - If you don't actively pursue level-ups, the game gets hard to play.

::right::

<SlidevVideo muted autoplay loop print-timestamp="3" print-poster="/mh-pr-hq-print.jpg">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このプロジェクトはマッチ３パズルに RPG 的な要素を付け加えたカジュアルゲームです。このグリッドは、一番下の段だけがインタラクション可能で、クリックでブロックを壊せます。そしてブロックを３つ以上並べることで、それぞれのブロックが持つ効果を引き出すことができる、というシステムです。

RPG 的な成長要素があって、経験値を貯めることでレベルアップします。経験値は敵を倒すだけでなく、鍵を使って宝箱を開けたり、多くのブロックをいっぺんに消したりすることで稼げます。敵は徐々に強くなっていくので、うまく経験値を稼いでいかないと、段々とプレイが難しくなっていく、という内容になっています。
-->

---
layout: image-right
image: /mh-background.jpg
---

# Development Background

- Aimed for finished quality as a vertical slice.
- Deliberately chose a safe, familiar game concept.
- "Can we properly build the kind of game we've always made?"

<!--
開発背景についてですが、前回のプロジェクトを通して Unity AI の使い方は大体分かってきたので、今回のプロジェクトでは、もう少し本格的にゲームとして作り込んでみようと考えました。規模として大きなものを作る余裕は無かったんですが、バーティカル・スライスとして、規模を限定しながらも完成クオリティのものを目指す、という方針です。

その目的のため、ゲーム内容としては実験的なものではなく、既にありそうなものを敢えて選びました。今まで手作業で作ってきたようなものを、AI エージェントを使ってちゃんと作ることができるのかどうか確かめたかった、ということですね。
-->

---
layout: image-right
image: /mh-heroes.png
---

# Development Background

- Used Unity Lite
- Generated almost all assets
- Used AI Assistant for Editor operations too
- Built in about 2 weeks

<!--
まだこの段階でも、Unity Lite モデルしか存在していませんでしたので、Unity Lite を全ての作業に使用しました。前のプロジェクトと同じく、ほぼ全てのアセットを Generator で生成しています。今回は約２週間で完成させました。
-->

---

<div class="h-full flex flex-col">

# Development Process

<div class="flex-1 min-h-0 flex items-center justify-center">
<svg width="800" height="169" viewBox="10 108 900 190" fill="none">
<defs>
<marker id="tlAh" viewBox="0 0 10 10" markerWidth="6" markerHeight="6" refX="9" refY="5" orient="auto">
<path d="M0 0 L10 5 L0 10 Z" fill="currentColor" stroke="none" />
</marker>
<marker id="tlB" viewBox="0 0 10 10" markerWidth="7.5" markerHeight="7.5" refX="9" refY="5" orient="auto">
<path d="M0 0 L10 5 L0 10 Z" fill="#39AAFF" stroke="none" />
</marker>
<marker id="tlO" viewBox="0 0 10 10" markerWidth="5.25" markerHeight="5.25" refX="9" refY="5" orient="auto">
<path d="M0 0 L10 5 L0 10 Z" fill="#e67e22" stroke="none" />
</marker>
</defs>
<path d="M40 220 C 84 87, 172 87, 216 214" stroke="#39AAFF" stroke-width="2" marker-end="url(#tlB)" />
<text x="130" y="286" text-anchor="middle" style="font-size:17px" fill="currentColor">Puzzle part prototype</text>
<text x="130" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">Plan &amp; execute</text>
<text x="333" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">Incremental changes</text>
<path d="M230 220 C 240 173, 258 173, 268 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M272 220 C 282 173, 300 173, 310 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M314 220 C 324 173, 342 173, 352 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M356 220 C 366 173, 384 173, 394 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M398 220 C 408 173, 426 173, 436 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M450 220 C 494 87, 582 87, 626 214" stroke="#39AAFF" stroke-width="2" marker-end="url(#tlB)" />
<text x="540" y="286" text-anchor="middle" style="font-size:17px" fill="currentColor">RPG part prototype</text>
<text x="540" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">Plan &amp; execute</text>
<text x="743" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">Incremental changes</text>
<path d="M640 220 C 650 173, 668 173, 678 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M682 220 C 692 173, 710 173, 720 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M724 220 C 734 173, 752 173, 762 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M766 220 C 776 173, 794 173, 804 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M808 220 C 818 173, 836 173, 846 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<line x1="20" y1="228" x2="890" y2="228" stroke="currentColor" stroke-width="2" marker-end="url(#tlAh)" />
<line x1="33" y1="220" x2="33" y2="236" stroke="currentColor" stroke-width="2" opacity="0.6" />
<line x1="223" y1="220" x2="223" y2="236" stroke="currentColor" stroke-width="2" opacity="0.6" />
<line x1="443" y1="220" x2="443" y2="236" stroke="currentColor" stroke-width="2" opacity="0.6" />
<line x1="633" y1="220" x2="633" y2="236" stroke="currentColor" stroke-width="2" opacity="0.6" />
<line x1="853" y1="220" x2="853" y2="236" stroke="currentColor" stroke-width="2" opacity="0.6" />
</svg>
</div>

</div>

<!--
次にこのプロジェクトの開発の流れについて解説します。この図は開発のタイムラインを大まかに視覚化したものです。

まず最初に長めのプロンプトを使って one shot でパズル部分のプロトタイプを作成しました。いきなり RPG と融合した形で始めるのではなく、まず最初にパズルゲームとして成立するかどうかを検証したわけですね。ここでは AI Assistant の Plan モードを使ってプラン・ドキュメントを作成してから、それに従って実行するという流れで作業しました。

そこから先は、短めのプロンプトを繰り返してインクリメンタルに改良を続けます。そしてパズルゲーム部分がある程度完成したら、次に RPG 部分のプロトタイプを作成しました。ここでも長めのプロンプトと Plan モードを使用しています。

それが完成したら、また短くインクリメンタルな作業を繰り返して、内容を作り込んでいく……と言う感じですね。

このように、要所要所で大きな作業を Plan モードで実行しながら、それ以外の部分では細かくインクリメンタルな作業を繰り返す、と言うスタイルで開発作業を進めました。

この時はまだ Unity Lite モデルしか使えなかったので、全ての作業を Unity Lite で行っています。今であれば、大きな作業は Unity Default や Unity Ultra を使用して、細かな作業は Unity Lite を使用する、と言うような使い分けが良いのかもしれませんね。
-->

---

# Puzzle Part Prompt

<blockquote>

이 프로젝트에서는 이른바 매치3 퍼즐과 RPG가 융합된 게임을 개발합니다. 이를 위해 우선 매치3 퍼즐 부분의 게임성을 검증할 수 있도록, 퍼즐 부분만 구현한 프로토타입을 만들기로 합니다. 이 매치3 퍼즐은 다음과 같습니다.

- 7x7 보드에 블록이 가득 채워져 있다
- 블록의 종류는 검(공격), 방패(방어), 마법, 회복, 보석, 열쇠, 꽝(효과 없음)의 7종류
  - 단, 프로토타입 단계에서는 에셋 생성을 피하기 위해 각 블록에 빨강, 파랑, 보라, 초록, 노랑, 회색 색을 할당해 단색 스프라이트로 대체한다.
- 플레이어는 맨 아래 행에만 간섭할 수 있다
- 그 간섭 방법이란 클릭한 블록을 파괴하는 것이다.
- 조작으로 블록을 파괴한 경우 그 효과는 발동되지 않는다.
- 블록이 파괴되면 그 위에 있는 모든 블록이 낙하한다
- 낙하 후 매치 판정이 이루어지고, 3개 이상 이어진 블록은 소멸한다.
- 이때 소멸한 블록의 효과가 발동된다.
- 블록 소멸이 발생한 경우, 그로 인해 생긴 빈 공간을 채우도록 블록이 위에서 등장(낙하)한다
- 조작으로 블록을 파괴한 경우에도 마찬가지로 블록이 보충되지만, 이때는 '꽝' 블록의 출현율이 높아진다
  - 반대로 매치 시의 블록 보충에서는 효과가 있는 블록만 등장한다

</blockquote>

<!--
例として最初のパズル部分のプロンプトの内容を紹介します。時間が限られているので詳しく内容は見ませんが、大体これくらいの文章量でプロトタイプを作成した、というわけです。
-->

---

# RPG Part Prototype

<blockquote>

이 게임은 매치3 퍼즐과 RPG의 융합을 목표로 하지만, 본격적인 RPG를 구현하는 것이 아니라 RPG의 전투 부분만 반복하면서 경험치를 모아 레벨업해 나가는, RPG 전투를 본뜬 리소스 관리 게임을 지향합니다. 이 RPG 전투 부분의 프로토타이핑을 위해, 성장 요소는 일단 무시하고, 어쨌든 적이 반복해서 등장해 전투를 벌이는 부분만 만들고자 합니다.

핵심이 되는 요소를 아래에 적습니다.

## 파라미터

적은 개별적으로 히트 포인트를 가지며, 0이 된 적부터 사망합니다. 주인공 파티는 파티 전체로 통합된 히트 포인트를 가지며, 0이 되면 파티 전멸이 됩니다.

적은 종류별로 공격력을 가집니다. 주인공 파티의 공격력은 현재로서는 고정으로 합니다(성장 요소를 구현하지 않기 때문).

방어력이라는 개념은 존재하지 않으며, 히트 포인트만으로 강함이 표현됩니다.

주인공 파티는 히트 포인트와는 별도로 Shield 카운터를 가집니다. 이를 통해 적의 공격을 상쇄할 수 있습니다.

...

</blockquote>

<!--
次に紹介するのは RPG 要素のプロトタイプを行った際のプロンプトです。こちらはかなり長い内容になっています。必要な要素を列挙していますが、細かな実装方法までは指定していません。まだ次のページに続きます。
-->

---

<blockquote>

...

주인공 파티는 경험치를 가집니다. 프로토타입 단계에서는 의미가 없습니다(상태 관리만 해 주세요)

주인공 파티는 Key 보유 플래그를 가집니다. 이는 보물상자를 여는 데 필요하지만, 프로토타입 단계에서는 의미가 없습니다(상태 관리만 해 주세요)

## 이벤트 큐

적의 행동과 주인공 파티의 행동(블록 소멸에 의해 발생하는 것)은 이벤트 큐에 푸시되어 순서대로 처리됩니다. 단, 주인공 파티의 행동은 큐에 쌓여 있는 적의 행동 앞에 끼어들도록 삽입됩니다.

## 행동의 종류

Zombie Mage 이외의 적은 직접 공격을 합니다. 공격력만큼의 데미지가 발생하지만, 탱커의 방어로 상쇄할 수 있습니다.

Zombie Mage는 마법 공격을 합니다. 이 공격은 탱커에 의해 방어되지 않습니다. 반드시 데미지를 입힙니다.

주인공 파티는 Sword 블록을 지웠을 때 Fighter의 직접 공격이 발생합니다. 지운 블록 수에 비례한 데미지가 발생합니다.

...

</blockquote>

<!--
まだこの先も続きますね。

ここに列挙されているような要素は、相互に関係し合っている部分があるので、インクリメンタルに作業すると、かえって複雑になってしまうかもしれない、と思いました。なので、ある程度まとめて作業してもらうわけですね。
-->

---

<blockquote>

...

Shield 블록을 지웠을 때 Tank의 방어가 발생합니다. 지운 블록 수만큼 Shield 카운터가 증가합니다.

Heal 블록을 지웠을 때 회복이 발생합니다. 지운 블록 수에 비례한 히트 포인트 회복이 이루어집니다.

Gem 블록을 지웠을 때 경험치 획득이 발생합니다. 지운 블록 수에 비례해 경험치가 증가합니다.

Key 블록을 지웠을 때 열쇠 획득이 발생합니다. 열쇠는 플래그 관리만 하므로 지운 블록 수는 관계없으며, 이미 보유한 상태에서 지워도 변화하지 않습니다. 단, 보너스로 경험치가 증가합니다.

## '꽝' 블록의 효력

블록 소멸에 휘말려 지워진 '꽝' 블록은 일반 블록의 1/3 효력을 가지는 것으로 합니다. 그 계산에서 소수점 이하는 버림으로 합니다.

## 적의 출현

적을 전멸시킬 때마다 새로운 적 무리가 출현합니다. 현재로서는 적의 수는 2~5 사이의 랜덤으로 하고, 출현하는 적의 종류도 완전 랜덤으로 해 주세요.

</blockquote>

<!--
これで終わりです。このプロジェクトでは最長のプロンプトですね。最も重いタスクだったと思います。
-->

---
layout: image-right
image: /mh-director-designer.png
---

# Short Prompt Examples

<blockquote>
글자가 조금 너무 큰 것 같으니 절반 크기로 줄여 주세요.
</blockquote>

<blockquote>
느낌은 좋은데, 조금 더 빠르게 하는 편이 좋겠습니다. 0.4초 동안 두 번 부드럽게 빛나도록 변경해 주세요.
</blockquote>

<blockquote>
글자가 등장할 때의 연출에 약간의 움직임을 주고 싶습니다. 살짝 위에서 떨어져 통통 튀는 움직임을 넣어 주세요. 그리고 사라질 때까지의 시간도 조금 줄이고 싶습니다. 등장 애니메이션부터 소멸이 끝날 때까지 총 1초 안에 들어가도록 해 볼까요.
</blockquote>

<blockquote>
느낌 좋네요! 다만 좀 더 절도 있게 만들고 싶으니, 반사 시의 감쇠율을 높여 봐 줄 수 있나요?
</blockquote>

<!--
次は、短いインクリメンタルな作業に使ったプロンプトを抜き出してみました。先ほどのような長いプロンプトを使うことは稀で、ほとんどの作業はこのような短いプロンプトを使って、細かな変更を積み重ねていくことで進めていきました。

まあ本当に、ディレクターがプログラマーやアーティストの後ろに貼り付いて、口頭で指示するような感じですね。ゲーム開発の現場では時折こういった光景を見かけるので、それとそっくりだなと思いました。
-->

---
layout: section
---

# Asset Production Workflow

<!--
次に Unity AI の Generator を使ったアセット制作の流れについて触れたいと思います。
-->

---
layout: image-right
image: /mh-generator-models.png
---

# Available Models

- A wide variety of models to choose from
- For image generation, Gemini 3.0 Pro and Gemini 3.1 Nano Banana 2 get the most use

<!--
Generator には様々な生成モデルがカタログ的に並べられていて、用途に合わせて使い分けることができるようになっています。ただ、色々な事情があって、実際に使用するモデルは一部に限られてくると思います。

例えば、画像生成であれば、Gemini 3.0 Pro, Gemini 3.1 Nano Banana 2 を使う機会が圧倒的に多いかなと思います。というのも、ローカル言語、つまり日本語や韓国語を問題無く使うことのできる画像生成モデルって、この辺りに限られてくるんですよね。それに加えて、表現力の高さや編集能力の高さを考慮すると、どうしてもこれらのモデルの使用頻度が高くなります。
-->

---
layout: image-right
image: /mh-image-board.png
---

# Creating an Image Board

- Establish the look within a single image
  - Keeping a consistent look across separate images is difficult

<!--
そしてまず最初に行うのはイメージボードの作成ですね。これは、キャラクターなどをバラバラに作成すると、そのスタイルや方向性が散逸してしまうので、１枚の絵の中に収めて生成することで、それを防ぐというアプローチです。ベースとなる統一されたイメージをここで固めてしまうわけですね。

このイメージボードのまとめ方については、プロジェクトの方針次第になりますが、今回はプレイヤーパーティーのイメージボードと、敵モンスターのイメージボードを、それぞれ独立して作成しました。
-->

---

# Creating Each Character

- Cut out individual characters
- Generate animations with video generation models
  - Converted into 4x4 sprite sheets
  - Trial and error takes considerable time
- Apply a background removal model
  - Avoid semi-transparency — it's hard to handle

<div class="flex items-center justify-center gap-3 mt-8">
  <img src="/mh-golem-base.jpg" class="w-36 rounded" />
  <div class="text-2xl opacity-60">→</div>
  <SlidevVideo muted autoplay loop class="w-36 rounded" print-poster="/mh-golem-attack-print.jpg">
    <source src="/mh-golem-attack.mp4" type="video/mp4" />
  </SlidevVideo>
  <div class="text-2xl opacity-60">→</div>
  <img src="/mh-golem-attack.jpg" class="w-36 rounded" />
  <div class="text-2xl opacity-60">→</div>
  <img src="/mh-golem-attack-alpha.jpg" class="w-36 rounded" />
</div>

<!--
イメージボードができたら、そこから各キャラクタを切り出して、独立したスプライトに変換します。この切り出し作業も、Nano Banana を使用しました。切り出し作業のついでに、ポーズや表情の調整を行っています。

そして、これらのベースとなるスプライトからアニメーションを生成します。Unity AI の Generator では Kling や Seedance などの動画生成モデルが使えます。Generator は生成された動画から 16 個のフレームをサンプリングして、スプライトシートとしてベイクします。

ただ、これらの動画生成モデルを使ったことのある方なら分かると思うんですが、生成にはかなりのコツが必要です。思った通りの動きを作るのはなかなか難しいと思いますし、生成に時間もかかるので、試行錯誤にかなり根気が必要となります。恐らく、想像以上に時間とクレジットを消費することになると思いますので、そこは注意してください。

そして最後に背景透過モデルを適用して完成です。この背景透過モデルもちょっとクセがあるので、最初は注意が必要です。特に半透明の表現を扱うのが難しいですね。煙や炎のような半透明の表現を使いたい場合は注意して下さい。
-->

---

# Generating Sound Effects

- Used ElevenLabs SFX
- No local language support (English required)
  - Hard to convey nuance
- Generation is fast, so iteration is easy

<div class="flex items-center justify-center gap-4 mt-6">
  <video controls class="flex-1 min-w-0 rounded">
    <source src="/mh-sfx-hit.mp4" type="video/mp4" />
  </video>
  <video controls class="flex-1 min-w-0 rounded">
    <source src="/mh-sfx-magic.mp4" type="video/mp4" />
  </video>
</div>

<!--
次に効果音を生成します。Unity AI の Generator では効果音専用のモデルとして Elevenlabs SFX モデルが提供されているので、これを使うことになります。

このモデルでは日本語や韓国語は使えません。英語を使用する必要があります。しかしこの、効果音を英語で表現するというのは、想像以上に難しいと感じました。我々は擬音を使って音を表現することに慣れてしまっているので、英語の文章で音をどう表現したらいいのかよく分からないんですよね。

ただ、生成速度は早いので、繰り返し試行錯誤していくことでなんとかしました。

作成例をちょっとお見せします。最初は攻撃のヒット音ですね。これは "Flesh impact hit sound, punchy and heavy" というプロンプトで生成したものです。

次のは魔法攻撃がヒットした時の音ですね。本当はもっと神秘的な感じにしようと思ったんですが、それだとダメージの痛みが伝わらないと思って、結局、シンプルな破裂音にしました。
-->

---
layout: image-right
image: /mh-audio-tailor.png
---

# Editing Sound Effects

- Generated sounds come with inconsistent characteristics
  - Unneeded silent sections
  - Varying volume levels
  - Unwanted fade-in/out on loop sounds

- Developed a dedicated tool
  - github.com/keijiro/AudioTailor
  - Trims silence
  - Normalizes volume
  - Loop conversion

<!--
こうして AI モデルによって生成されたオーディオクリップには、不要な無音部分が含まれていたり、音量が小さ過ぎたりすることがあります。そのままでも使えないことはないですが、調整が難しくなる可能性があります。

そこで、このようなオーディオクリップの仕様のバラつきを自動的に整えるツールを作成しました。それがこの AudioTailor パッケージです。AI モデルで生成した効果音を使う場合に便利なツールだと思います。ぜひ活用して下さい。
-->

---
layout: two-cols-video
---

# Creating Particle Effects

- Created Particle Systems with AI Assistant
- Works fine for simple particle motion

::right::

<SlidevVideo muted autoplay loop print-poster="/mh-particle-system-print.jpg">
  <source src="/mh-particle-system.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このプロジェクトではパーティクルエフェクトも AI Assistant を使って作成しました。すごく凝った動きとか特殊なエフェクトを作るのは難しいですが、ごく一般的な動きのパーティクルエフェクトであれば、十分対応可能です。この動画のような典型的なエフェクトであれば、スプライト素材の生成も含めて AI Assistant に作ってもらうことができます。
-->

---
layout: image-right
image: /mh-custom-shader.png
---

# Generating Shaders

- Text-based unlit shaders can be generated without any issues

<!--
シェーダーも AI Assistant で作成しています。HLSL ベースの Unlit シェーダーであれば、問題無く生成できます。

ここで作成したのは、スプライトを指定した色で塗り潰す、というシェーダーです。標準のスプライトシェーダーは tint color を使って色を変えることはできるのですが、完全に指定した色で塗り潰すということはできません。キャラクターがフラッシュする演出などで、このような単純な塗り潰しを使いたかったので、カスタムシェーダーが必要になったわけです。

このようにライティングを行わない Unlit シェーダーであれば問題無いのですが、ライティングを行う Lit シェーダーでは少し問題が発生します。このことについては次のプロジェクトで詳しく触れます。
-->

---
hide: true
---

<div class="h-full flex flex-col">

# On Style

- Didn't use the KinoEight effect this time.
- Wanted to see if stylistic cohesion could be achieved without relying on special effects.
- Largely succeeded, but the "AI look" feels a bit stronger.

<img src="/mh-game-over.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
ちなみに少し余談になるのですが、このプロジェクトでは、前に解説した KinoEight エフェクトを敢えて使用しませんでした。そういった特殊なエフェクトに頼らずに、アートスタイルの統合感を出せるかどうか確かめたかったためです。

実際に、丁寧にイメージボードなどを用意することで、ある程度の統合感は実現できたと考えています。ただしその反面、ある種の「AI 臭さ」というか…… Nano Banana を使ったことのある方なら分かるかもしれませんが、「これって何だか Nano Banana っぽいな」と感じさせるクセというか雰囲気というか、そういうのがあるんですよね。これについては、エフェクトを外したことや、制御しやすいスタイルに統一していったことによって、少し強まってしまっている気がします。

この辺りをどうバランスしていくか、というのは、今後の課題になっています。
-->

---
layout: section
hide: true
---

# Other Applications

<!--
最後に、その他のちょっと変わった AI Assistant の応用について触れたいと思います。
-->

---
layout: image-right
image: /mh-game-balance-tool.png
hide: true
---

# Game Balance Tuning Tool

- A tool to see how parameter changes affect difficulty
- Consolidated related parameters into a single Scriptable Object
- Built the UI as its custom editor

<!--
このプロジェクトでは、最初にマッチ３パズル部分を作ってから、そこに RPG 的な要素を追加していったわけですが、その RPG 部分のゲームバランスを調整するにあたって、専用のツールを AI Assistant に作ってもらいました。

これはゲーム内のパラメーター、例えばレベルアップに必要な経験値や、レベルアップで増加するヒットポイントの量とかですね、そういったものを変更すると、その結果として難易度がどのように変化するのか、シミュレートして表示してくれるツールです。RPG 的な成長要素のあるゲームは、ちょっとした数値の変更で手応えが大きく変化するので、この手のツールを用意することはとても重要になると思います。

実装は簡単で、ゲームバランスに関連するパラメーターを単一の ScriptableObject に集約したうえで、そのカスタムエディタとしてこのような UI を構築するように指示しました。

このようなゲームデザインの補助ツールを即席で作れるのは AI assisted なゲーム開発の利点だと思いますし、エンジニア以外の方々が自分の作業を自分のアイデアによって、自力で効率化することができる、というのは、開発体験の向上に大きく寄与できるものだと思います。
-->

---
layout: section
hide: true
---

# Wrap-Up

<!--
最後にこのプロジェクトのまとめです。
-->

---
hide: true
---

# Project Retrospective

- Confidence that "games can be developed with Unity AI"

- Recognized the limitations of Unity Lite (at that point)
  - The context window filled up quickly
  - Long-sustained tasks were hard to execute

<div class="flex items-center justify-center gap-3 mt-8">
  <img src="/mh-context-window.png" class="w-60 rounded" />
</div>

<!--
このプロジェクトを通して、ゲームのプロトタイプやカジュアルゲームなら Unity AI と Unity Lite の組み合わせで十分に開発できるという手応えが得られました。

その反面、軽量モデルである Unity Lite の制約に気付くこともありました。僕がこのプロジェクトで使用した限りでは、推論能力についてはそれほど問題にならなかったのですが、どちらかと言うとコンテキストウィンドウが埋まってしまいやすいと感じることの方が多かったです。作業を続けるうちにコンテキストが埋まってしまって、新しいコンテキストへ移行せざるを得ない、と言うタイミングが度々発生してしまったんですね。

ただこれは、AI Assistant 自体の挙動の調整や、サブエージェントへの対応などが行われたことによって、今はだいぶ改善されています。また、より高性能な Unity Default モデルが登場したことによって、負荷の高い場面ではモデルを切り替えるという対処も可能になりました。
-->

---
layout: chapter
---

<BgVideo src="/dm-pr-hq.mp4" />

# Project: Drift Mayhem

<!--
それでは３つ目のゲームプロジェクト、Drift Mayhem について解説したいと思います。
-->

---
layout: two-cols-video
---

# Game Overview

- "Wouldn't it be cool to riddle enemies with a machine gun while pulling off drifts?"
- A prototype to validate the idea
- Bare minimum content as a game

::right::

<SlidevVideo muted autoplay loop print-timestamp="3" print-poster="/dm-pr-hq-print.jpg">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このゲームは「ドリフトをきめながらマシンガンで敵を撃ちまくったらカッコいいのではないか」というアイデアを思いついて、それを検証するために作ったプロジェクトです。まさにこのアイデアを検証するために必要な部分だけを実装しました。敵も一種類しか存在しませんし、プレイヤー側の操作も最低限のものしか実装されていません。

それでも実際に作ってみることで、これは楽しくてカッコいいし、ゲームとして面白くなりそうだ、という手応えをちゃんと得ることができました。
-->

---

<div class="h-full flex flex-col">

# Development Background

- Used Unity Default
- First attempt at 3D game development
  - Evaluating Tripo P1
- Short development period (effectively 3 days)

<div class="flex-1 min-h-0 flex items-center justify-center">
  <img src="/dm-buggy-design.png" class="rounded w-80" />
</div>

</div>

<!--
このプロジェクトでは初めて Unity Default モデルを使用しています。

また、このプロジェクトでは初めて 3D ゲームの開発にも挑戦しています。これはまた後で解説しますが、3D モデル生成用の Generator として Tripo P1 が使えるようになったので、これを試したかったというのが動機としてあります。

このプロジェクトは最短期間で検証を済ませたかったので、制作期間はかなり短いです。実質的に３日間ぐらいの作業で済ませています。
-->

---
layout: section
---

# Development Process

<!--
次に開発の流れについてですが、基本的な考えは前のプロジェクトと変わりません。ここでは、このプロジェクトで初めて取り組んだ要素や、このプロジェクトならではのユニークな要素について、かいつまんで解説していきます。
-->

---
layout: two-cols-video
---

# Infinite Terrain Generation System

- Auto-generating an "endless wasteland"

<blockquote>

다음으로 지면을 무한 생성하는 시스템을 구축합니다. 적당한 범위(10m x 10m 등)를 1세그먼트로 취급하고, 이를 16x16 정도의 적당한 해상도의 그리드로 만듭니다.

..

이 그리드에는 적당한 프랙탈 노이즈 함수를 사용해 자연스러운 굴곡을 부여합니다. 그리고 자기 차량이 있는 세그먼트 주위의 세그먼트를 동적으로 생성해 나감으로써, 무한히 달려도 지면이 이어지도록 합니다. 이때 세그먼트 사이에 이음매가 생기지 않도록 주의해 주세요. 이러한 무한 지면 시스템의 구현 플랜을 세워 주세요.
</blockquote>

::right::

<SlidevVideo muted autoplay loop print-poster="/dm-ground-generation-print.jpg">
  <source src="/dm-ground-generation.mp4" type="video/mp4" />
</SlidevVideo>

<!--
まず最初にプロシージャルな無限地形生成システムを作ってもらいました。荒野を走り回りながら次々に敵を倒していく、という内容にしたかったので、地形を無限に生成できるようにする必要があったわけです。

プロンプトはこんな感じで、Plan Mode でプランを立ててから、それを実行しました。

これについては特に問題無く一発で実装できました。あとはパラメーターをいくつか増やしたりというような調整を行っただけです。
-->

---
layout: two-cols-video
---

# Terrain Shader

- Needed a URP Lit shader that applies vertex colors
- Implementing URP Lit shaders is hard
  - Tons of boilerplate
  - Subtle differences between versions
- Too difficult for Unity Default

::right::

<SlidevVideo muted autoplay loop print-poster="/dm-wrong-shader-print.jpg">
  <source src="/dm-wrong-shader.mp4" type="video/mp4" />
</SlidevVideo>

<!--
今回はローポリ風の絵作りを目指していたので、最初は地面に何もテクスチャを貼らずに動かしていました。ただそれだと、移動したときのスピード感が得られにくいという問題があります。そこで、頂点カラーを使った簡単なチェッカー模様を付けることにしました。

ここで問題となったのが、頂点カラーを適用するカスタムシェーダーの作成です。この地面には陰影を付けたり影を落としたりしたいので、URP Lit シェーダーにする必要があります。

これは、実は AI にはかなり難しい作業です。というのも、URP Lit シェーダーを作るには、大量のボイラープレート的なコードを扱う必要があります。しかもそれは最新バージョンの URP に対応している必要があります。AI の持つ、ちょっと古い知識では、それを完全に正しく実装するのは難しいかもしれません。

いちど試しに Unity Default モデルに URP Lit シェーダーを生成してみてもらったのですが、色々と不具合が発生したので止めておきました。


この動画は失敗したシェーダーの例ですが、奇妙な黒い帯が現れてしまっていますよね。恐らくシャドウのカスケードの境界がおかしくなっているのだと思います。
-->

---
layout: image-right
image: /dm-shader-graph.png
---

# Workaround

- Manually created a simple Shader Graph

<!--
今回は、実現したいことは非常に簡単な内容だったため、ここで無理はせず、Shader Graph を手動で作成することで解決しました。たったこれだけのシェーダーですね。

このように僕の場合はシェーダーの内容が簡単だったので手作業で回避できましたが、複雑なシェーダーを AI に作ってもらいたい、という場合はどのようにすれば良いのでしょうか？ 実は Unity 6.5 以降であれば手軽な解決方法があります。
-->

---

<div class="h-full flex flex-col">

# Shader Function Reflection API

- Turns HLSL shaders into custom nodes
- Available in Unity 6.5 and later

<img src="/dm-shader-reflection.jpg" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
それが Shader Function Reflection API です。これは、HLSL シェーダーにコメントとしてリフレクション情報を埋め込む、という仕組みです。これによって、HLSL シェーダー関数を Shader Graph のカスタムノードとして直接使うことが可能になります。

これを使って、複雑なシェーダーコードは AI に書いてもらいつつ、シェーダーの入出力との接続は Shader Graph 上で行う、という分担が可能になるわけですね。

もちろん将来的には Shader Graph との繋ぎ込みも自動化したいところですが、とりあえず現状ではこのような手段をとることが可能になっています。
-->

---
layout: two-cols-video
---

# Refining the Car Behavior

- The first prototype used pseudo-physics behavior

<blockquote>
🤖 현재 구현은 단일 Rigidbody에 직접 힘을 가하는 '유사 물리(아케이드 스타일)'로 구성되어 있습니다.
</blockquote>

<blockquote>
🤖 오프로드 게임을 개발할 때 Unity의 WheelCollider를 사용할지 여부는 매우 중요한 설계상의 분기점입니다. 결론부터 말씀드리면, 이 프로젝트에서는 현재의 '단일 Rigidbody 기반 유사 물리' 접근 방식을 압도적으로 추천합니다.
</blockquote>

- Deliberately instructed it to use real physics

::right::

<SlidevVideo muted autoplay loop print-poster="/dm-physics-arcade-style-print.jpg">
  <source src="/dm-physics-arcade-style.mp4" type="video/mp4" />
</SlidevVideo>

<!--
次に車の挙動の作り込みを行いました。実は、AI エージェントは最初のプロトタイプとして、擬似物理、いわゆるアーケードスタイルの挙動を実装してきました。車輪のシミュレーションを行わず、単一の rigid body で擬似的に車の動きを表現する、というものです。

これは実際に賢い選択で、今回のようにリアリティを重視しない内容で、非現実的なドリフト挙動などがコンセプトに盛り込まれている場合、理にかなっている判断だと思います。一般論で言えば、擬似物理の方が制御の自由度が高くて、調整もしやすいはずなんですよね。

ただ、擬似物理を選択したことによって、車輪のサスペンションがまったく効かず、地面の凹凸に引っ掛かりやすい挙動になってしまっていました。また、僕としては、こういったゲームで物理挙動を使った場合の破天荒な動きにも、面白さや遊びの余地があると考えています。

そこで、ここでは敢えてリアルな物理挙動を使ってほしいと AI エージェントに指示して、作り直してもらうことにしました。

こういった感じで、AI が理にかなった選択をしてくれるんだけど、現実問題としてそれじゃダメなんだよなー、と感じることが時折あります。この物理挙動の問題は、このプロジェクトにおける象徴的な出来事でした。
-->

---
layout: video
video: /dm-drift-prototype.mp4
---

# Initial Drift Behavior

<!--
次に、このプロジェクトのコアとなる、ドリフトの挙動を実装することになります。ロックオンした敵の方を向きながらスライドしていくような挙動を組むわけですね。まずは何も指示せずに AI エージェント任せで作ってみてもらったのですが、こんな感じになりました。まあ一応それっぽい挙動になってはいるんですが、敵にロックオンしている感じがちょっと弱いかなと思います。もっと力強くスライドしながら、それでも敵を狙い続ける、というような激しさが欲しいと思いました。
-->

---
layout: video
video: /dm-drift-rework.mp4
---

# Improving the Drift Behavior

<!--
そこで次は、明確に指示を出して改良してみることにしました。アイデアとしては、Configurable Joint を使って敵と車体を束縛してしまう、というものです。分かりやすく言うと、敵と自分をロープで縛って、グルッとスイングするような動きにしてしまう感じですね。かなり強引ですがシンプルな解決法です。

これは制御が容易である反面、ガッチリと固定されているような感じが出てしまうので、動きが不自然になりやすいです。このテスト動画でも、ちょっと動きが固くなってしまっている感じがありますね。でもこの辺りは、細かい調整と演出次第で何とかなるものです。

ここでも先ほどと同じく、AI がバランスの取れたものを作ってくれるんだけど、それに対して、もっと割り切ってしまうように人間からアドバイスする、という構図になっていますね。
-->

---
layout: video
video: /dm-drift-finished.mp4
---

<!--
その後、調整を繰り返して、最終的に出来たのがこのドリフト挙動です。基本的な仕組みは前のページのバージョンとほとんど変わっていないんですが、調整と演出で見え方が大きく変わってくるのが分かりますね。
-->

---
hide: true
---

# Impact of Unity Default

- Essentially no context rebuilds
- Better work continuity compared to past projects

<!--
さて、ここまでの作業で Unity Default モデルを使用した感想を簡単にまとめておきます。以前のプロジェクトではタスク毎にコンテキストを新規作成するような使い方が多かったですが、このプロジェクトでは基本的にコンテキストを作り直すことなく作業を続けることができました。毎日、最初にコンテキストを作成したら、その上で一日作業を続ける、という感じですね。過去のプロジェクトと比較して、持続した作業を行うことが容易になったと感じます。

また、基本的な推論能力もかなり向上していると感じました。これについては定量的な比較を行っていないので、あくまでも感覚的な話になってしまうのですが、指示した内容を正しく汲んで、正しい作業を行ってくれていると言う感覚があります。もちろん、先ほども触れたように、その判断を敢えて変える必要もあったわけですが、その判断に至るまでの道筋はちゃんと正しく実行してくれている、と言う感じです。
-->

---
layout: section
---

# Asset Production Workflow

<!--
次に Drift Mayhem におけるアセット制作の流れについて、前のプロジェクトと異なる点のみ触れたいと思います。
-->

---
layout: image-right
image: /dm-tripo-generation.png
---

# 3D Model Generation

- Used Tripo P1
- Controllable triangle count
- Clean topology
- glTF binary format (.glb)
  - Imported with the glTFast package
  - Supports embedded textures

<!--
このプロジェクトでは 3D モデルの生成に Tripo P1 モデルを使用しました。このプロジェクトを開始する少し前に使用可能になったので、早速試してみたというわけです。

Tripo P1 は他の汎用的な 3D 生成モデルと比較して、ゲーム開発に最適化された特性をいくつも備えています。トライアングル数に上限を設けることができますし、比較的綺麗なトポロジーのメッシュを生成することができます。

出力形式としては glTF のバイナリ形式である .glb 形式を使用し、Unity 側では glTFast パッケージを使用してインポートしています。.glb 形式を使うのは、テクスチャデータをファイルに埋め込むことができるからです。これによって、Tripo P1 からテクスチャとマテリアルまで含めて単一の .glb ファイルとして出力することができます。
-->

---
layout: image-right
image: /dm-model-generation.png
---

# 3D Model Generation Workflow

- Create an image board
- Split into parts
- Generate a model for each part

<!--
Tripo P1 は入力画像を必要とするので、まず最初にイメージボードを作成します。これには普通のスプライトと同じように Nano Banana などの画像生成モデルを使います。

次にパーツへの分解を行います。この車体は屋根に砲塔があるのと、あとはタイヤをそれぞれ独立して回転させる必要があるので、これらのパーツを独立した画像に分割します。この分割にも Nano Banana などの編集機能のある画像生成モデルを使います。

最後に、それぞれのモデルを Tripo P1 で生成します。
-->

---
layout: image-right
image: /dm-glb-embedded-texture.png
---

# Embedded Texture Issues

- Beware of .glb embedded textures
  - They become high-resolution uncompressed textures
  - The settings can't be changed

<!--
こうして生成された .glb ファイルを Unity で使用する際に、注意すべき点がひとつあります。それは、埋め込まれたテクスチャが、高解像度の非圧縮テクスチャになってしまうということです。例えばこの車体のテクスチャは、カラーだけで 21.3MB も使っています。

これはメモリを余計に消費するというだけでなく、配布するアプリのサイズも大きくなってしまいます。特に Web ブラウザゲームではアプリサイズを気にしますから、このことは無視できません。
-->

---
layout: image-right
image: /dm-glb-embedded-texture-tweaked.png
---

# Fix: glTFast Tweaks

- Created a tool that overrides the settings
- github.com/keijiro/glTFastTweaks

<!--
そこで、このインポート設定をオーバーライドするためのツールを作成しました。glTFast Tweaks という名前のパッケージです。このツールは glTFast のアドオンとして動作して、テクスチャのインポートの際にその設定を書き換えることができます。これで画像サイズを縮小したり、テクスチャ圧縮を有効化したりできます。

例えばこの車体のテクスチャであれば、21.3MB あったのを、リサイズとテクスチャ圧縮によって 0.7MB まで減らすことができました。

このようにビルドサイズを大きく減らすことができますので、ぜひ活用して下さい。
-->

---
layout: two-cols
---

# Music (BGM)

- Lyria 3 music generation model
- Can generate music that holds together as music
- Used for the game-start jingle

::right::

<div class="h-full flex items-center justify-center">
  <video controls class="w-full">
    <source src="/dm-lyria3-example.mp4" type="video/mp4" />
  </video>
</div>

<!--
もうひとつ、最近利用が可能になったモデルに Lyria 3 音楽生成モデルがあります。今までちゃんとした音楽を生成できるモデルは存在しなかったんですが、これでようやく BGM などが作れるようになりました。

ちょっとサンプルを再生してみましょうか。（再生）。こんな感じで、もっともらしい曲を生成することができます。

ただし、ちょっと曲の展開に違和感があったり、単調さが目立ってしまうことがあるかなと思いました。ものすごい名曲を生み出せるわけではない、と考えた方が良いと思います。

ただ、プロトタイプとして、とりあえず何か音を入れておきたい、という用途には十分だと思います。今回はイントロ部分だけを切り取って、ゲーム開始時のジングルとして使用しました。
-->

---
layout: section
hide: true
---

# Wrap-Up

<!--
最後にこのプロジェクトのまとめを述べておきたいと思います。
-->

---
layout: image-right
image: /dm-hello-unity-default.png
hide: true
---

# Improved Practicality

- Agent: Unity Default
- 3D Model: Tripo P1
- Music: Lyria 3

<!--
この Drift Mayhem プロジェクトでは、過去のプロジェクトよりも進化した新しいモデル群を使用することができました。Unity Default モデル、Tripo P1 モデル、Lyria 3 モデル、などですね。

対話型の開発アプローチにおいて Unity Default は十分な性能を提供してくれましたし、Tripo P1 はゲームに使いやすい仕様の 3D モデルを生成してくれました。これらのモデルを活用することで、3D ゲームにおいても効率の良いプロトタイピングが可能になったと感じます。
-->

---
layout: image-right
image: /dm-dirty-code.png
hide: true
---

# Code Degradation

- Prioritized implementation; cleanup was deferred
- Did no refactoring at all
- As a result, the code degraded significantly
  - Many remnants of old specs remain
  - Names don't match functionality
  - etc...

<!--
ただ今回は、非常に短期間にコーディング作業を重ねていったので、コードの劣化が無視できないレベルになってしまいました。一応、動くコードにはなっているのですが、実態としてはとても汚い状態になっています。クラス名やメソッド名が機能と一致していなかったり、重複する機能の実装が存在していたり、使用していない古い仕様の残骸が残っていたり、様々です。

例えば、このプロジェクトでは敵のオブジェクトを表す言葉として "Target", "Dummy", "Enemy", "Drone" という単語が混在しています。それぞれが何を意味するのか整理しないまま、仕様の追加を重ねていったので、実態が分かりにくくなっています。コードとしては非常に危険な状態ですね。

これらの劣化したコードは、ここから更に開発を続けるならば、整理を行う必要があります。というのも、AI エージェントも結局は人間と同じように、クラス名やメソッド名、コメントなどを手掛かりに開発を進めていくので、そこに混乱があれば、AI もまた混乱してしまいます。結局は、人間の読みやすいコードであることが AI にとっても重要である、ということですね。
-->

---
layout: image-right
image: /dm-dirty-code2.png
hide: true
---

# Missing Unity Development Practices

- No object pooling
- Effects built with piles of Rigid Bodies

<!--
また、Unity の使い方としても、一般的な開発プラクティスを疎かにした状態になってしまっています。例えば、弾丸の Game Object はオブジェクトプールを使用せずに毎回使い捨てになっています。

また、この火花のエフェクトは Particle System ではなく、このキューブ一つ一つが Game Object になっていて、それぞれに Mesh Filter と Mesh Renderer と Rigid Body が付与されています。ものすごく贅沢な作り方というか……こういう作り方をしてはいけない、とよく言われることを、そのままやってしまっていますよね。

この辺りも、ここから先へ開発を進めていくならば、改善が必要でしょう。
-->

---
hide: true
---

# The Importance of Refactoring

- It can fix things properly when instructed to.
- Code tends to degrade when implementation continues without pause.
- Serious ongoing development requires deliberate refactoring.

<!--
もちろん AI エージェントは、これが良くない状態であることを知っていて、改善方法も正しく把握しています。改善して下さいと指示すれば、問題なく改善してくれるでしょう。ただ、そう伝えない限りは、人間から与えられた実装作業の方を優先する、という感じですね。なので、あれを作って下さい、これを作って下さい、と次々に指示を続けていると、リファクタリングする機会を失ってしまうことが多いようです。

Unity を使用してきたユーザーの皆さんだったら、こういった危険な状態を察知することができると思います。ただ、例えば Unity AI を使って初めて Unity を触る、というような場合には、ここは落とし穴になるかもしれません。

AI エージェントに対して定期的に設計のチェックやリファクタリングを行うよう指示するなど、対策を講じていく必要があるかもしれません。
-->

---
layout: chapter
---

<BgVideo src="/ms-demo-hq.mp4" />

# Project: Mesh Slicer

<!--
さて、最後のプロジェクト、Mesh Slicer について解説したいと思います。
-->

---

<div class="h-full flex flex-col">

# Project Overview

- Tech demo
- Slicing 3D models with arbitrary planes
- Interactive demo

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3" print-poster="/ms-demo-hq-print.jpg">
  <source src="/ms-demo-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
今までのプロジェクトはゲームをテーマとしてきましたが、最後のこれだけは純粋に技術的なデモです。3D メッシュオブジェクトを任意の平面で切断すると言う機能を実装しました。また、そのインタラクティブデモとして、マウス操作で物理オブジェクトを切り刻める、と言うものを作ってみました。
-->

---

<div class="h-full flex flex-col">

# Development Background

- Testing long-running tasks with the MCP Server and an external agent

<div class="flex-1 min-h-0 flex items-center justify-center">
  <svg width="600" height="190" viewBox="-120 0 600 190" fill="none" stroke="currentColor" stroke-width="2">
    <defs>
      <marker id="ahB72" viewBox="0 0 10 10" markerWidth="6" markerHeight="6" refX="9" refY="5" orient="auto">
        <path d="M0 0 L10 5 L0 10 Z" fill="currentColor" stroke="none" />
      </marker>
    </defs>
    <text x="35" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🧑</text>
    <text x="195" y="108" text-anchor="middle" dominant-baseline="central" style="font-size:58px" stroke="none" fill="currentColor">🤖</text>
    <path d="M73 108 H157" marker-end="url(#ahB72)" stroke-linecap="round" />
    <path d="M195 146 V161 Q195 171 205 171 H265 Q275 171 275 161 V38 Q275 28 265 28 H205 Q195 28 195 38 V70" marker-end="url(#ahB72)" stroke-linecap="round" stroke-linejoin="round" />
    <text x="115" y="76" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">📄</text>
    <text x="300" y="100" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">⚙️</text>
    <text x="345" y="100" text-anchor="middle" dominant-baseline="central" style="font-size:34px" stroke="none" fill="currentColor">🕐</text>
  </svg>
</div>

</div>

<!--
開発背景についてですが、このプロジェクトは MCP Server を利用した長時間タスクの自律的な実行を試すために始めたものです。

フロンティア AI モデルを使用した開発においては、数十分とか数時間とかいった、長時間に渡るタスクの実行も珍しくありません。

現状の Unity の AI エージェントは、このような用途には特化されていません。もしこれを実践したいと思ったら、外部の AI エージェントから MCP を使って Unity Editor と連携する必要があります。

それを実際に試してみたわけですね。
-->

---

# Testability

- Long-running tasks require automated testing
- Separate out the parts that can be auto-tested

<!--
そして、このような長時間タスクの自律的な実行において必須となるのが testability の確保です。つまり、自動テストによって検証が可能でなければいけない、ということですね。そうでなければ、人間によるチェックが必要になってしまって、そこで自律的な実行は止まってしまいます。

このプロジェクトでもインタラクティブデモの部分は人間の手による検証が必要なので、そこは分離して考えることにしました。
-->

---
layout: two-cols
---

# Project Components

- MeshSlicer class
  - Slices a Mesh with an arbitrary plane
  - Comes with automated tests
  - Built with Unity MCP Server + Claude Code (Opus 4.8)

- SlicingDemo scene
  - Interactive demo
  - Built with AI Assistant (Unity Lite)

::right::

<div class="flex flex-col items-center justify-center gap-4" style="height: 394px">
  <img src="/ms-projects-work.png" class="flex-1 min-h-0 max-w-full object-contain rounded shadow" />
  <img src="/ms-projects-demo.jpg" class="flex-1 min-h-0 max-w-full object-contain rounded shadow" />
</div>

<!--
以上を前提に、このプロジェクトの構成要素を解説します。

まずは MeshSlicer クラスが存在します。これは Mesh の切断機能を提供するものです。Test Runner による自動テストが用意されていて、動作検証までを AI エージェントが自律的に行えるようになっています。そしてこの部分は MCP Server と Opus 4.8 を使用して、長時間タスクとして自律的に開発を行ってもらいました。

その後に、この機能を使ったインタラクティブデモとして SlicingDemo というシーンを AI Assistant で作成しました。これはシンプルな内容なので Unity Lite を使用しています。
-->

---

# Prompt

<blockquote>

Unity에서 메시 오브젝트를 임의의 평면으로 절단하는 기능을 구현해 주세요.

이 기능은 Mesh와 Unity.Mathematics.Geometry.Plane으로 표현되는 평면을 주면, 그 Mesh를 절단해 생기는 두 개의 Mesh를 생성해 반환합니다. 각 절단면에는 뚜껑이 추가됩니다.

소스가 되는 Mesh는 이른바 2-manifold/watertight 조건을 만족한다고 전제합니다.

정점 데이터는 position, normal, tangent, uv0까지 지원합니다. 절단면의 uv0은 (0,0) 고정으로 합니다.

여기서는 TDD적인 접근을 사용합니다. 즉, 기능 구현에 앞서 포괄적인 테스트를 구현해야 합니다. 테스트 실행에는 Unity 표준 Test Runner를 사용합니다.

테스트에는 볼록 메시뿐 아니라 단면이 여러 루프·중첩(구멍 뚫림/애뉼러스)이 되는 케이스를 포함합니다. 구체적으로는 토러스, 속이 빈 파이프, 열린 상자(트레이 형태), 볼(bowl) 형상을 포함해 각 단면에서 뚜껑이 올바르게 닫히는지 검증합니다. 또한 프로젝트에 포함된 fbx 모델도 사용합니다.

...
</blockquote>

<!--
これが実際に使用したプロンプトです。ざっくりと大まかに要件を伝えつつ、Test Driven Development, TDD 的な手法で進めるように指示しています。

まだもうちょっと続きがあります。
-->

---

<blockquote>
...

구현은 처음에는 최적화를 고려하지 않는 형태로 진행합니다. 여기서는 정확성을 중시하고 퍼포먼스는 고려하지 않습니다. 그 구현이 완성되면 Mesh Renderer를 사용해 씬에서 렌더링도 수행하고, 당신(AI 에이전트)의 시각을 활용한 정성적 검증도 수행합니다.

다음으로 퍼포먼스를 측정합니다. 여기서는 메서드 단독 퍼포먼스와 시스템 전체 퍼포먼스를 나누어 측정합니다. 후자는 적당량의 하이폴리 메시를 매 프레임 절단한 뒤 Mesh Renderer로 그림으로써 렌더링까지 포함한 부하를 측정합니다.

이것들이 완료된 후 최적화를 시작합니다. 여기서는 Burst 컴파일러, C# Job System을 사용하면서 NativeArray와 Advanced Mesh API를 활용해 배열 복사를 최대한 줄이는 방안을 도입합니다. 앞서 설명한 퍼포먼스 측정 방법으로 그 효과를 확인합니다. 몇 차례 최적화를 반복해 보고, 타당한 성과가 얻어진 시점에 작업을 완료합니다.

</blockquote>

<!--
続きの部分では開発の流れを伝えていますね。最初はパフォーマンスを考えずに実装を行うように指示しています。そして、それをベースに最適化を行って、結果を比較するように指示していますね。

つまり、計画、実行、評価、改良、というようなループを自律的に回すわけです。
-->

---

<div class="h-full flex flex-col">

<SlidevVideo muted autoplay controls class="flex-1 min-h-0 w-full object-contain" print-poster="/ms-long-session-print.jpg">
  <source src="/ms-long-session.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
これは実際に実行している様子を早回しにしたものです。完了までに約50分費やしています。今どきの長時間タスクでは何時間も自律的に実行するケースがザラにあるので、これはまあ、まだ短い方だと思います。

完了しましたね。ここに結果が表示されています。
-->

---

<div class="h-full flex flex-col">

<div class="flex-1 min-h-0 flex flex-col justify-center">

#### Performance (20,480-triangle icosphere, Editor)

| Naive | Burst | Speedup |
|---|---|---|
| 9.16 ms | 1.04 ms | 8.8x |

</div>

</div>

<!--
この結果を転載したのがこちらです。Burst 対応によってパフォーマンスが 8.8 倍に改善されたようですね。

このあと、AI Assistant を使ってインタラクティブデモの部分を作ったわけですが、その部分については、今までのプロジェクトと同様なので割愛します。
-->

---
layout: two-cols-video
---

# Bug Discovery and Diagnosis

- A bug where holes appear at certain angles

::right::

<SlidevVideo muted autoplay loop print-poster="/ms-corner-cases-print.jpg">
  <source src="/ms-corner-cases.mp4" type="video/mp4" />
</SlidevVideo>

<!--
これで完成しました、となればハッピーエンドなのですが、実際にはそう上手くはいきませんでした。一見うまく動いているのですが、たまに切断面に穴が生じるという不具合が発生しました。

これを検証するために、切断面を手動で操作できるツールを作ってもらい、不具合の生じる条件を特定しました。そして、その条件をもとに、AI エージェントに原因を特定してもらいました。
-->

---

<div class="h-full flex flex-col">

<div class="flex-1 min-h-0 flex items-center justify-center degen-fig">
<svg width="820" viewBox="0 70 720 160" role="img" aria-label="Degeneracy when the plane passes through a vertex, and its avoidance by offsetting">
<g transform="translate(20,20)">
<line x1="0" y1="140" x2="310" y2="140" class="sp dash"/>
<polyline points="20,60 90,140 160,70 230,150 290,95" class="sk"/>
<circle cx="221" cy="140" r="3.5" class="dot-plane"/>
<circle cx="90" cy="140" r="3.5" class="dot-bad"/>
<circle cx="90" cy="140" r="8" class="ring-bad"/>
<line x1="86" y1="150" x2="72" y2="180" class="leader"/>
<text x="70" y="198" class="mid small tbad">vertex exactly on the plane</text>
</g>
<g transform="translate(390,20)">
<line x1="0" y1="140" x2="310" y2="140" class="sp dash faint"/>
<line x1="0" y1="120" x2="310" y2="120" class="sp dash"/>
<polyline points="20,60 90,140 160,70 230,150 290,95" class="sk"/>
<circle cx="72" cy="120" r="3.5" class="dot-plane"/>
<circle cx="110" cy="120" r="3.5" class="dot-plane"/>
<circle cx="204" cy="120" r="3.5" class="dot-plane"/>
<circle cx="263" cy="120" r="3.5" class="dot-plane"/>
<line x1="14" y1="138" x2="14" y2="126" class="sp"/>
<polygon points="14,118 9.5,127 18.5,127" class="fp"/>
<text x="24" y="130" class="small tplane">m·ε</text>
</g>
</svg>
</div>

</div>

<style>
.degen-fig {
  --plane: #A294F0;
  --bad: #E5675F;
  --ink: #E2E7EA;
  --muted: #97A2AB;
}
.degen-fig svg text { font-family: inherit; font-size: 12.5px; fill: var(--muted); }
.degen-fig svg .small { font-size: 11px; }
.degen-fig svg .mid { text-anchor: middle; }
.degen-fig svg .tplane { fill: var(--plane); font-weight: 600; }
.degen-fig svg .tbad { fill: var(--bad); font-weight: 600; }
.degen-fig svg .sk { stroke: var(--ink); stroke-width: 1.8; fill: none; }
.degen-fig svg .sp { stroke: var(--plane); stroke-width: 1.6; fill: none; }
.degen-fig svg .fp { fill: var(--plane); }
.degen-fig svg .dash { stroke-dasharray: 7 5; }
.degen-fig svg .faint { opacity: .32; }
.degen-fig svg .leader { stroke: var(--muted); stroke-width: 1; }
.degen-fig svg .dot-plane { fill: var(--plane); }
.degen-fig svg .dot-bad { fill: var(--bad); }
.degen-fig svg .ring-bad { fill: none; stroke: var(--bad); stroke-width: 2; }
</style>

<!--
調査の結果、切断面にぴったりと接する頂点やエッジがある場合に失敗することがある、というのが分かりました。この問題に対する解決法も色々と提示されましたが、どれも少し負荷の高いものでした。

そこで、代替案として切断面のオフセットによるワークアラウンドを、僕の方から提案しました。このようなエッジケースを検出したら、切断面をずらすことで問題を回避してしまおう、というものですね。ゲーム向けの用途であれば、このような妥協は許容できます。

このワークアラウンドは効果てきめんで、その結果、先ほど動画でお見せしたような、安定した動作を得ることができました。
-->

---
layout: section
hide: true
---

# Other Features Used

<!--
次に、このプロジェクトのインタラクティブデモの作成でいくつかの Unity AI の機能を利用したので、それについて触れておきたいと思います。
-->

---
hide: true
---

<div class="h-full flex flex-col">

# MCP Tools (MCP clients)

- Used Blender to convert models into sliceable ones
- Controlled Blender from AI Assistant via MCP
  - Used `blender-mcp`

<img src="/ms-mcp-client.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
まず利用したのは MCP Tools の機能です。これは AI Assistant から外部の MCP クライアントを利用するというものです。

これは MCP Server の機能と混同しないように気をつけて下さい。こっちは MCP クライアントを利用する機能ですね。 Unity 内の AI Assistant から外部のツールを、例えばここでは Blender を、MCP で操作するわけです。

ここでは 3D モデルを、いわゆる「マニフォールドモデル」に変換するのに使用しました。つまり「切断可能なタイプのモデル」に変換する処理ですね。AI Assistant から Blender を操作して、Blender 上でその変換を行ってもらうようにしました。
-->

---
hide: true
---

<div class="h-full flex flex-col">

<img src="/ms-mcp-config.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
MCP Tools 設定は Project Settings の中にあります。この "Enable MCP Tools" をオンにしたうえで、ここにある "mcp.json" ファイルに設定を加えます。うまく設定できれば、この "Servers" の所に Blender が出現するはずです。
-->

---
hide: true
---

<div class="h-full flex flex-col">

# Project Skills

<img src="/ms-skill-config.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
また、その Blender 上での操作手順については、AI Assistant のスキル機能を活用することにしました。

スキルというのは、AI エージェントによくある機能ですが、ツールの使い方や定型的な手続きを教えるための仕組みですね。これによって、Blender の機能をどういう風に呼び出せばマニフォールドモデルに変換できるのか、教え込む事ができるわけです。

このようなプロジェクト毎のスキルは Assets の Skills ディレクトリの中に配置します。

スキル関係の設定は Preferences の中にあります。ここに作成したプロジェクトスキルが表示されるはずです。デフォルトでは "Deny" になっているので "Allow" に変更しましょう。

このように MCP Tools とスキルの組み合わせによって、マニフォールドモデル変換が完全に自動化されました。AI Assistant に「このモデルをスライス可能にして」と命令すれば、あとは勝手に Blender を呼び出して変換してくれるわけです。

このように、AI Assistant の MCP Tools 機能とスキル機能は、外部アプリやサービスとの連携を自動化するにあたって便利な機能です。そのような要素がある場合にはぜひ活用してください。
-->

---
hide: true
---

# Wrap-Up

- The MCP Server is handy for running long tasks with external agents
- MCP Tools and Skills are handy for integrating with external tools

<!--
まとめです。このように、MCP Server を使用することによって、外部エージェントを使った長時間タスクの実行が可能になります。最近は Unity AI でもフロンティアグレードのモデルが使えるので、必ずしも外部のエージェントを使わなくてはならないという訳ではないですが、長時間タスクの実行や開発ループの構築に関しては、最新の知見を利用できるメジャーな AI エージェントの方に利があるのかなと思いました。

また、MCP Tools 機能については、Unity AI Assistant から外部ツールを操作するのに使えることが分かりました。その手続きを整理するのにカスタムスキル機能が便利であることも確認できました。
-->

---

<div class="h-full grid grid-cols-2 grid-rows-2 gap-2">

<SlidevVideo muted autoplay loop class="w-full h-full object-cover" print-timestamp="3" print-poster="/mm-pr-hq-print.jpg">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<SlidevVideo muted autoplay loop class="w-full h-full object-cover" print-timestamp="3" print-poster="/mh-pr-hq-print.jpg">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<SlidevVideo muted autoplay loop class="w-full h-full object-cover" print-timestamp="3" print-poster="/dm-pr-hq-print.jpg">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<SlidevVideo muted autoplay loop class="w-full h-full object-cover" print-timestamp="3" print-poster="/ms-demo-hq-print.jpg">
  <source src="/ms-demo-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
さて、最後の方は駆け足になりましたが、４つのプロジェクトについてお話ししてきました。

AI については技術の進化が激しく、状況は刻々と変化しています。僕がこの資料を用意している間にも様々な変化がありましたし、今後も変化が続くはずです。これが正解、と言う確固たる答えは存在しなくて、頻繁に自分の考えを更新していく必要があります。

このような変化に対応するには、みんなでその考えを共有していくことが大切だと思います。ぜひ皆さんの考えも様々なチャンネルを通して共有して頂ければと思います。
-->

---

<img src="/unite-thankyou-bg.jpg" class="absolute inset-0 w-full h-full object-cover" style="transform: scaleY(-1)" />

<div class="absolute flex items-center" style="left:7%; top:21.9%; width:30.9%; height:56.4%">
  <h1 style="font-size:49px; line-height:1.25">Thank you</h1>
</div>

<div class="absolute bg-white" style="left:54%; top:26.8%; width:26%; height:46.2%"></div>

<!--
以上で僕のセッションは終了です。ご清聴ありがとうございました。
-->
