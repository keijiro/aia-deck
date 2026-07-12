---
theme: seriph
title: Unity AI Examples
colorSchema: dark
class: text-center

drawings:
  persist: false

transition: slide-left

comark: true

duration: 40min

fonts:
  sans: Inter
  provider: google
---

# Developing with Unity AI:<br>Practical Use Cases

<!--
みなさんこんにちは。Unity Technologies Japan の高橋啓治郎と申します。

このセッションでは Unity AI を実際のプロジェクトで使用した体験についてお話しします。僕は Unity AI を実際に幾つかのゲームプロジェクトや技術デモの制作に使用しました。そこで Unity AI が実際のプロジェクト開発においてどのように使えるのか、ということについて、様々な知見を得ることができました。今日はそれらの知見について皆さんと共有したいと思います。
-->

---
layout: section
---

# プロジェクトの紹介

<!--
それではまず始めに、実際に Unity AI を使用して開発したプロジェクトを、順番に紹介していきます。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover" print-timestamp="3">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Mirror Mage

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
まず最初のこのプロジェクトは "Mirror Mage" というカジュアルゲームです。敵の攻撃を反射して、それを攻撃に使う、というちょっと変わったシステムのアクションゲームです。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover" print-timestamp="3">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Dungeon Match Heroes

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
次のプロジェクトは "Dungeon Match Heroes" というカジュアルゲームです。マッチ３パズルゲームに RPG のエッセンスを加えたようなゲームですね。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover" print-timestamp="3">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Drift Mayhem

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
３つ目は "Drift Mayhem" という、オフロードカー・シミュレーションとシューティングが融合したようなゲームのプロトタイプですね。
-->

---

<div class="h-full flex flex-col">

# Mesh Slicer

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3">
  <source src="/ms-demo-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
そして最後に、これはゲームではなく技術デモですが、Mesh Slicer というプロジェクトです。3D モデルをマウスで切断する処理を開発して、それのインタラクティブデモを作成しました。
-->

---
layout: section
---

# 開発アプローチの分類

<!--
さて、これらのプロジェクトの解説に入る前に、AI エージェントを使った開発アプローチの分類について触れたいと思います。

というのも、AI エージェントをゲーム開発に使用するにあたっては、そのエージェントの使い方・動かし方について、いくつかの異なるアプローチが存在すると考えています。
-->

---

<div class="h-full flex flex-col">

<div class="flex-1 min-h-0 flex items-center justify-center gap-16">

<div class="flex flex-col items-center justify-center gap-8">
  <div class="text-xl">対話的</div>
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
  <div class="text-xl">自律的</div>
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
<div class="text-lg font-bold">対話的</div>
</div>
<div class="text-lg text-center">主力／軽量モデル</div>
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
<div class="text-lg font-bold">自律的</div>
</div>
<div class="text-lg text-center">フロンティアモデル</div>
</div>
</div>

<!--
僕のプロジェクトでも 3D モデルのメッシュを切断するという処理には、文化的な判断や社会的な要素も存在しませんので、このカテゴリに属することになります。ここでは、人間の手を介在させない、自律的開発のアプローチが有効になり得ます。ここでは Opus 4.8 のようなフロンティアモデルを使用しました。

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

# ゲーム概要

- 防御魔法しか使えない魔法使いを主人公とした、いわゆる "Survivor" 系ゲーム。
- 敵弾をバリアで反射させて、それを敵に当てることで、敵を倒せる。
- 経験値を貯めてレベルアップ。能力を選択して成長させることができる。

::right::

<SlidevVideo muted autoplay loop print-timestamp="3">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このゲームは、防御魔法しか使えない魔法使いを主人公とした、いわゆる "Survivor" 系のアクションゲームです。敵の攻撃を、この魔法陣バリアで跳ね返すことができます。跳ね返した弾にはコリジョンがあって、これを敵に当てることで、敵を倒せます。

主人公は経験値を貯めることでレベルアップします。レベルアップの際にライフが回復するほか、スキルを選択してパワーアップさせることができます。例えば、移動速度を速くしたり、バリアの大きさを大きくしたり、というようなことですね。
-->

---
layout: image-right
image: /mm-bg.png
---

# 開発背景

- 最初の Unity AI 作例
- Unity Lite を使用
- ほぼ全てのアセットを生成
- Editor 操作も AI Assistant を使用
- 約 10 日間で制作

<!--
このプロジェクトの開発背景を少し話しておきたいと思います。これは個人的に初めて作った Unity AI の作例でした。当時はまだ Unity Lite モデルしか存在していなかったので、すべての作業を Unity Lite で行なっています。

プロジェクト内で使用しているアセットは基本的にすべて Unity AI で生成しています。C# スクリプトやシェーダーは AI Assistant で作成していますし、スプライトや、それをアニメーションさせるためのスプライトシート、効果音などもすべて Generator で作成しました。

また、AI Assistant にどこまで作業を任せられるか知りたかったので、Unity Editor 自体の操作もほとんど AI Assistant に任せるようにしました。結果的に、自分の手で Hierarchy や Scene View を操作することは殆どありませんでした。

これは特に締め切りのないプロジェクトだったので、ゆっくりと制作を行なって、約１０日間でこのような形になりました。
-->

---
layout: section
---

# 開発の流れ

<!--
次にこのプロジェクトの開発の流れについて解説していきますが、これは最初のプロジェクトなので、本当に概要だけサラッと流していきましょう。
-->

---

<div class="h-full flex flex-col">

# 最初のプロトタイプ

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="10">
  <source src="/mm-reflex-shooter.mp4" type="video/mp4" />
</SlidevVideo>

<!--
まず最初に作成したプロトタイプは、こんな感じでした。全然違うゲームだったのが分かると思います。「敵の弾を反射して利用する」というコアのメカニクスは同じなのですが、最初は SF 風のテーマの 2D シューティングゲームとして作っていました。

ゲームエンジンをテストする際に 2D シューティングゲームというのは最も無難な題材のひとつですが、本当にシンプルなシューティングゲームだと挑戦的な要素が無くなってしまうので、ちょっとだけ捻って、この反射攻撃というアイデアを組み込んでみたわけです。
-->

</div>

---

# プロトタイプのプロンプト

<blockquote>
次のような 2D シューティングゲームを作成して下さい。

- 自機はマウスカーソルをある速度以下で滑らかに追いかける。
- 敵は画面外周囲から登場し自機に迫ってくる。
- 敵はかなりの密度で弾を撃ってくるが、自機を完全に狙うのではなく、ある程度バラけた撃ち方をしてくる。
- 自機は弾に衝突すると爆発する。
  - 爆発後は一定時間後にゲームを最初から再開する。
- 自機はマウスボタンを押している間、反射バリアを展開する。
- 反射バリアを展開している間、自機のエネルギーは減り続ける。
- 自機のエネルギーは、反射バリアを消してから、自機を静止させることで徐々に回復する。
- 反射バリアに当たった敵弾は跳ね返される。その時、敵弾の速度は倍増される。
- 跳ね返された敵弾は敵に対しての当たり判定を持ち、敵を破壊できる。
- アートスタイルとしては Sci-Fi を基本のテーマとする。

</blockquote>

<!--
このプロトタイプは、こんな感じのプロンプトで、ほぼ one shot で作成しました。Unity Lite のような軽量モデルでも、この程度のタスクなら難なくこなせますね。
-->

---

<div class="h-full flex flex-col">

# 方針転換

- シューティングゲームとしての伸び代が感じられず、どう発展させるべきか見えなかった。
- そこで思い切って、いわゆる "Survivors" 系のゲームとして作り替えることにした。

<img src="/mm-design-change.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
ただ、このプロトタイプを実際に作ってみて感じたのですが、シューティングゲームとしての伸び代が感じられなくて、この後どう発展させていくべきか分からなくなってきました。

そこで、ここで大幅な方針転換を行うことにしました。古典的なシューティングゲームではなく、いわゆる "Survivors" 系のゲームとして作り替えてみよう、と考えたわけです。

この方針転換によって大きく道がひらけました。顔の無い宇宙船ではなく、分かりやすく人格の見えるキャラクターになって、またそこから、防御しかできないことの物語的必然性が生まれました。パワーアップ要素は RPG 的な成長要素として組み込むことができるようになりましたし、スキルツリーなどの要素を今後追加していくことも可能だと思います。

このような大きな方針転換は、従来であれば精神的負荷の高い大変な作業であったと思いますが、AI assisted なゲーム開発アプローチであれば、その負荷はだいぶ軽くなります。特に今回のように初期プロトタイプの段階であれば、容易に転換が可能です。

こうして、素早くプロトタイピングを行いながら、人間の手によって評価を行い、人間のアイデアによって改良を重ね、自分たちの求める内容へと近付けていく、というアプローチが可能なのだなと、このプロジェクトで実感することができました。
-->

---

<div class="h-full flex flex-col">

# レトロゲーム風エフェクト

- 過去に開発した "KinoEight" エフェクトを使用

<img src="/mm-filter-comparison.png" class="flex-1 min-h-0 w-full object-contain mt-4" style="image-rendering: pixelated;" />

</div>

<!--
次に、このプロジェクトで使用したレトロゲーム風エフェクトについて触れておきたいと思います。

このプロジェクトでは、過去に僕が開発した "KinoEight" エフェクトを使って、このレトロゲーム風の見た目を作り出しています。この左側の画像がエフェクト無しの状態のもので、右側の画像がエフェクトを適用した状態のものです。使用する色の数や解像度を落とした上でディザリングをかけることで、この見た目を作り出しています。
-->

---

<div class="h-full flex flex-col">

# エフェクトを入れた理由

- 単にレトロゲーム風にしたかったわけではない。
- アセットの持つ「情報量の密度」の均一化が狙い。
- 統合感の無さを感じさせる要因になる。

<img src="/mm-style-comparison.png" class="flex-1 min-h-0 w-full object-contain mt-4" style="image-rendering: pixelated;" />

</div>

<!--
このエフェクトを入れた理由ですが、実は、レトロゲーム風の見た目にしたかったわけではありません。他の理由があります。それは「アセットの持つ情報密度の均一化」です。

これは、体型付けられた理論ではありませんし、教科書に載っているようなことでもなく、僕が勝手に言っていることなので、話半分に聞いてもらいたいのですが、スプライトなどの画像アセットの見た目を印象付ける要素の一つとして、「情報量の密度」というものがあります。それは例えば、絵としての描き込みの細かさや、色彩の深さなどを表しています。

そして、この情報密度がアセットによってバラバラだと、それらのアセットを統合している感覚が薄れてしまいます。何か寄せ集めを切り貼りしたような、コラージュ的な見た目になってしまうんですね。

例えば、この主人公のスプライトと、敵キャラクタのスプライト、背景の画像を並べてみると、一応スタイルを寄せる努力はしているんですが、それでも書き込みの密度や色彩の使い方にかなりバラつきがが出てしまったと感じました。
-->

---

<div class="h-full flex flex-col">

# 情報密度の均一化

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
これを強制的に均一化するテクニックとして、「一旦すべてのアセットの情報量を削って落とす」というものがあります。情報密度の低い方に合わせることによって、統合された感じを生み出そうというわけですね。

今回使用した KinoEight エフェクトは、解像度と色彩を強制的に落とすことによって、そのような効果を生み出すことができると考えています。

ただしこれは、品質を劣化させることで見た目を揃える、ということなので、実はあまり使いたくないテクニックせす。今回は Unity AI を使うのが初めてだったので、安直なテクニックに頼ってみた、という感じです。
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

# ゲーム概要

- マッチ３パズルと RPG の融合。
- グリッドの最下行のブロックのみ、クリックで崩すことができる。
- ブロックを揃えることで、それぞれのブロックが持つ効果を引き出す。
  - 剣ブロック＝攻撃、薬ブロック＝回復、など
- 経験値を貯めてレベルアップ。
  - 積極的にレベルアップを狙わないと、プレイが難しくなる。

::right::

<SlidevVideo muted autoplay loop print-timestamp="3">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このプロジェクトはマッチ３パズルに RPG 的なエッセンスを付け加えたようなカジュアルゲームです。このグリッドは、一番下の段だけがインタラクション可能で、クリックすることでブロックを壊せます。これを壊してブロックを３つ以上並べることで、それぞれのブロックが持つ効果を引き出すことができる、というシステムです。

RPG 的な成長要素があって、経験値を貯めることでレベルアップします。経験値は敵を倒すだけでなく、鍵を使って宝箱を開けたり、多くのブロックをいっぺんに消したりすることで稼げます。敵は徐々に強くなっていくので、そうやってうまく経験値を稼いでいかないと、段々とプレイが難しくなっていく、という内容になっています。
-->

---
layout: image-right
image: /mh-background.jpg
---

# 開発背景

- バーティカル・スライスとして完成クオリティのものを目指した。
- ゲーム内容としては無難なもの、既にありそうなものを敢えて選んだ。
- 「今まで通りのものを、ちゃんと作ることはできるのか？」

<!--
開発背景についてですが、前回の Mirror Mage の開発を通して Unity AI の使い方は大体分かってきたので、今回のプロジェクトでは、もう少し本格的にゲームとして作り込んでみようと考えました。規模として大きなものを作る余裕は無かったんですが、バーティカル・スライスとして、規模を限定しながらも完成クオリティのものを目指す、という方針です。

その目的のため、ゲーム内容としては実験的なものではなく、既にありそうなものを敢えて選びました。今まで手で作ってきたようなものを、AI でちゃんと作ることができるのかどうか確かめたかった、ということですね。
-->

---
layout: image-right
image: /mh-heroes.png
---

# 開発背景

- Unity Lite を使用
- ほぼ全てのアセットを生成
- Editor 操作も AI Assistant を使用
- 約２週間で制作

<!--
まだこの段階でも、Unity Lite モデルしか存在していませんでしたので、Unity Lite を全ての作業に使用しました。前のプロジェクトと同じく、ほぼ全てのアセットを Generator で生成しています。今回は約２週間で完成させました。
-->

---

<div class="h-full flex flex-col">

# 開発の流れ

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
<text x="130" y="286" text-anchor="middle" style="font-size:17px" fill="currentColor">パズル部分プロトタイプ</text>
<text x="130" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">プラン＆実行</text>
<text x="333" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">インクリメンタルな変更</text>
<path d="M230 220 C 240 173, 258 173, 268 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M272 220 C 282 173, 300 173, 310 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M314 220 C 324 173, 342 173, 352 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M356 220 C 366 173, 384 173, 394 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M398 220 C 408 173, 426 173, 436 214" stroke="#e67e22" stroke-width="2" marker-end="url(#tlO)" />
<path d="M450 220 C 494 87, 582 87, 626 214" stroke="#39AAFF" stroke-width="2" marker-end="url(#tlB)" />
<text x="540" y="286" text-anchor="middle" style="font-size:17px" fill="currentColor">RPG 部分プロトタイプ</text>
<text x="540" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">プラン＆実行</text>
<text x="743" y="252" text-anchor="middle" style="font-size:15px" fill="currentColor" opacity="0.7">インクリメンタルな変更</text>
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
次にこのプロジェクトの開発の流れについて大まかに解説します。この図は開発のタイムラインを大雑把に視覚化したものです。

まず最初に長めのプロンプトを使ってワンショットでパズル部分のプロトタイプを作成しました。いきなり RPG 要素と融合した形で始めるのではなく、まず最初にパズルゲームとして成立するかどうかを検証したわけですね。ここでは AI Assistant の Plan モードを使ってプラン文書を作成してから、それに従って実行するという流れで作業しました。

そこから先は、短めのプロンプトを繰り返してインクリメンタルに改良を続けます。そしてパズルゲーム部分がある程度完成したら、次に RPG 部分のプロトタイプを作成しました。ここでも長めのプロンプトと Plan モードを使用しています。

それが完成したら、また短くインクリメンタルな作業を繰り返して、内容を作り込んでいく……と言う感じですね。

このように、要所要所で大きな作業を Plan モードで実行しながら、それ以外の部分では細かくインクリメンタルな作業を繰り返す、と言うスタイルで開発作業を進めました。

この時はまだ Unity Lite モデルしか使えなかったので、全ての作業を Unity Lite で行っています。今であれば、大きな作業は Unity Default や Ultra を使用して、細かな作業は Unity Lite を使用する、と言うような使い分けが良いかもしれません。
-->

---

<blockquote>

このプロジェクトでは、いわゆるマッチ３パズルと RPG の融合したゲームを開発します。それにあたって、まずはマッチ３パズル部分のゲーム性を検証するために、そのパズル部分のみを実装したプロトタイプを作成することにします。このマッチ３パズルは以下のようなものになります。

- 7x7 の盤面にブロックが敷き詰められている
- ブロックの種類は、剣（攻撃）、盾（防御）、魔法、回復、宝石、鍵、ハズレ（効果無し）の７種類
  - ただしプロトタイプの段階ではアセットの生成を避けるために、それぞれのブロックに赤、青、紫、緑、黄、灰、の色を割り当て、単色のスプライトで代用する。
- プレイヤーは一番下の行のみ干渉することができる
- その干渉方法とは、クリックしたブロックを破壊することである。
- ブロックを操作で破壊した場合は、その効果は発揮されない。
- ブロックが破壊されると、その上にある全てのブロックは落下する
- 落下後にマッチ判定が行われ、３つ以上連なっているブロックは消滅する。
- この時消滅したブロックの効果が発揮される。
- ブロックの消滅が発生した場合、それによって生じた余白を埋めるようにブロックが上から登場（落下）してくる
- ブロックを操作で破壊した場合も同様にブロックが補充されるが、この時は「ハズレ」ブロックの発生率が高くなる
  - 逆に、マッチ時のブロックの補充では効果のあるブロックだけが登場する

</blockquote>

<!--
例として最初のプロンプトの内容を紹介します。時間が限られているので詳しく内容を精査することは避けますが、大体このくらいの文章量で初期プランを作って、そこからタスクを開始した、という雰囲気が分かればと思います。
-->

---

<blockquote>

このゲームは３マッチパズルとRPGの融合を目指すわけですが、本格的なRPGを実装するわけではなく、RPGの戦闘部分だけを繰り返しながら、経験値を貯めてレベルアップしていくという、RPGの戦闘を模したリソース管理ゲームというものを目指しています。このRPGの戦闘部分についてプロトタイピングを行うために、成長要素は一旦無視して、とにかく敵が繰り返し出てきて戦闘を行う、という部分だけを作りたいと思います。

核となる要素を以下に記します。

## パラメーター

敵は個々にヒットポイントを持ち、０になったものから死亡します。主人公パーティーは、パーティー全体で統合されたヒットポイントを持ち、０になるとパーティー全滅となります。

敵は種類ごとに攻撃力を持ちます。主人公パーティーの攻撃力は、現状では固定とします（成長要素を実装しないため）。

防御力の概念は存在せず、ヒットポイントだけで強さが表現されます。

主人公パーティーはヒットポイントとは別にShieldカウンタを持ちます。これによって敵の攻撃を相殺することができます。

主人公パーティーは経験値を持ちます。プロトタイプの段階では意味がありません（状態管理のみ行って下さい）

主人公パーティーはKey保持フラグを持ちます。これは宝箱を開けるのに必要になりますが、プロトタイプの段階では意味がありません（状態管理のみ行って下さい）

...

</blockquote>

<!--
次に紹介するのは RPG 要素のプロトタイプを行った際のプロンプトですね。かなり長い内容になっていますが、揃えて欲しい要素だけを列挙して、細かい実装方法までは踏み込んでいません。まだ次のページに続きます。
-->

---

<blockquote>

...

## イベントキュー

敵の行動や主人公パーティーの行動（ブロックの消滅によって発生するもの）はイベントキューにプッシュされ、順番に処理されていきます。ただし主人公パーティーの行動については、キューに積まれている敵の行動の前に割り込むように挿入されます。

## 行動の種類

Zombie Mage 以外の敵は直接攻撃を行います。攻撃力分のダメージが発生しますが、タンクの防御によって相殺することができます。

Zombie Mage は魔法攻撃を行います。この攻撃はタンクによって防御されることがありません。必ずダメージを与えます。

主人公パーティーはSwordブロックを消した時、Fighterによる直接攻撃が発生します。消したブロックの数に比例したダメージが発生します。

Shield ブロックを消した時、Tank による防御が発生します。消したブロックの数だけShielfカウンタが増えます。

Heal ブロックを消した時、回復が発生します。消したブロックの数に比例したヒットポイント値の回復が生じます。

Gem ブロックを消した時、経験値の取得が発生します。消したブロックの数に比例して経験値が増えます。

...

</blockquote>

<!--
まだこの先も続きますね。これらの要素は相互に関係し合っている部分があるので、インクリメンタルに作業すると、かえってコンテキストが複雑になり過ぎるかもしれないなと思ったんですよね。そのため、ある程度一気に実装することにしました。
-->

---

<blockquote>

...

Key ブロックを消した時、鍵の取得が発生します。鍵はフラグ管理のみ行うため、消したブロックの数は関係ありませんし、既に保持している状態で消しても変化しません。ただし、ボーナスとして経験値が増えます。

## 「ハズレ」ブロックの効力

ブロックの消滅に巻き込まれて消された「ハズレ」ブロックは、通常ブロックの 1/3 の効力を持つものとします。その計算において小数点以下は切り捨てとします。

## 敵の出現

敵を全滅させるごとに新たな敵の集団が出現します。現状では敵の数は２〜５の間のランダムとし、出現する敵の種別も完全ランダムとして下さい。

</blockquote>

<!--
これで終わりです。かなり長いプロンプトでしたが、このプロジェクトでは最長のプロンプトですね。最も重いタスクだったと思います。
-->

---
layout: image-right
image: /mh-director-designer.png
---

# 短いプロンプト例

<blockquote>
文字が少し大き過ぎるように感じたので、半分のサイズにして下さい。
</blockquote>

<blockquote>
いい感じですが、もうちょっと早くしたほうが良さそうです。0.4秒で２回柔らかく光る、に変更してください。
</blockquote>

<blockquote>
文字が登場する際の演出に少し動きを与えたいと思います。少し上から落下してチョンチョンと跳ねる動きを付けて下さい。そして消滅までの時間も少し狭めたいです。登場アニメーションから消滅が終わるまでのトータルが１秒に収まるようにしてみましょうか。
</blockquote>

<blockquote>
いい感じです！ただもう少しキレをよくしたいので、反射時の減衰率を上げてみてもらえますか？
</blockquote>

<!--
次は、短いインクリメンタルな変更に使ったプロンプトを抜き出してみました。先ほどのような長いプロンプトを使うことは本当に稀で、ほとんどの作業はこのような短いプロンプトを使って、細かな変更を積み重ねていくことで進めていきました。

まあ本当に、ディレクターがプログラマーやアーティストの後ろに貼り付いて、口頭で指示するような感じですね。ゲーム開発の現場では時折こういった後継を見かけるので、それとそっくりだなと思いました。
-->

---
layout: section
---

# アセット制作の流れ

<!--
次に Unity AI の Generator を使ったアセット制作の流れについて触れたいと思います。
-->

---
layout: image-right
image: /mh-generator-models.png
---

# 使用可能モデル

- 様々なモデルが使用可能
- 画像生成は Gemini 3.0 Pro, Gemini 3.1 Nano Banana 2 の使用頻度が高い

<!--
Generator には様々な生成モデルがカタログ的に並べられていて、用途に合わせて使い分けることができるようになっています。ただ、色んな事情があって、実際には使用するモデルは一部に絞られてくると思います。

例えば、画像生成であれば、Gemini 3.0 Pro, Gemini 3.1 Nano Banana 2 を使う機会が圧倒的に多いかなと思います。というのも、ローカル言語、つまり韓国語や日本語を問題無く使うことのできる画像生成モデルって、この辺りに限られてくるんですよね。それに加えて、表現力の高さや編集能力の高さを考慮すると、どうしてもこれらのモデルの使用頻度が高くなります。
-->

---
layout: image-right
image: /mh-image-board.png
---

# イメージボードの作成

- １枚の画像でイメージを固める
  - バラバラの画像で統一したイメージを保つのは難しいため

<!--
そしてまず最初に行うのはイメージボードの作成ですね。これは、キャラクターなどをバラバラに作成すると、そのスタイルや方向性が散逸してしまうので、１枚の絵の中に収めて生成することで、それを防ぐというアプローチです。ベースとなる統一されたイメージをここで固めてしまうわけですね。

このイメージボードにどこまでの情報を含めるかは、プロジェクトの方針次第になると思いますが、今回はプレイヤーパーティーのイメージボードと、敵モンスターのイメージボードを、それぞれ独立して作成しました。
-->

---

# 各キャラクタの作成

- 単体のキャラクターの切り出し
- 動画生成モデルを使ってアニメーションを生成
  - 4x4 スプライトシートに変換
  - 試行錯誤にかなりの時間が必要とされる
- 背景透過モデルを適用
  - 半透明表現は難しいので避ける

<div class="flex items-center justify-center gap-3 mt-8">
  <img src="/mh-golem-base.jpg" class="w-36 rounded" />
  <div class="text-2xl opacity-60">→</div>
  <SlidevVideo muted autoplay loop class="w-36 rounded">
    <source src="/mh-golem-attack.mp4" type="video/mp4" />
  </SlidevVideo>
  <div class="text-2xl opacity-60">→</div>
  <img src="/mh-golem-attack.jpg" class="w-36 rounded" />
  <div class="text-2xl opacity-60">→</div>
  <img src="/mh-golem-attack-alpha.jpg" class="w-36 rounded" />
</div>

<!--
イメージボードができたら、そこから各キャラクタを切り出して、独立したスプライトに変換します。この切り出し作業は、普通に Photoshop を使ってもいいですし、Nano Banana で自動化することも可能です。

そして、これらのベースとなるスプライトからアニメーションを生成します。これには、Unity AI で Generator として提供されている Kling や Seedance などの動画生成モデルを使用することになります。Unity AI の Generator では、生成された動画から 16 個のフレームをサンプリングして、スプライトシートにベイクします。

ただ、これらの動画生成モデルを使ったことのある方なら分かると思うんですが、生成にはかなりのコツが必要です。思った通りの動きを作るのはなかなか難しいと思いますし、生成にも時間がかかるので、試行錯誤にはかなり根気が必要となります。恐らく、想像以上に時間とクレジットを消費することになると思いますので、そこは注意してください。

そして最後に背景透過モデルを適用して完成です。この背景透過モデルもちょっとクセがあるので、コツを覚えるまで試行錯誤が必要になるかもしれません。特に半透明の表現を扱うことが難しいですね。このゲームでも、本当は魔法や煙で半透明の表現を使いたかったんですが、そこは割り切って諦めています。
-->

---

# 効果音の生成

- ElevenLabs SFX を使用
- ローカル言語非対応（英語必須）
  - ニュアンスを伝えるのが難しい
- 生成は早いので試行錯誤は容易

<div class="flex items-center justify-center gap-4 mt-6">
  <video controls class="flex-1 min-w-0 rounded">
    <source src="/mh-sfx-hit.mp4" type="video/mp4" />
  </video>
  <video controls class="flex-1 min-w-0 rounded">
    <source src="/mh-sfx-magic.mp4" type="video/mp4" />
  </video>
</div>

<!--
次に効果音を生成します。Unity AI の Generator では効果音専用のモデルとして Elevenlabs SFX モデルが提供されているのでう、これを使うことになります。

このモデルでは韓国語や日本語を使うことはできませんので、英語を使用する必要があります。しかも、効果音を自然言語を使って表現するというのは、思った以上に難しいと感じました。長く詳細なプロンプトを書いてもニュアンスが伝わらないことが多かったです。短く端的に伝わる表現をボキャブラリとして覚えておいて、その組み合わせでなんとかする、というようなアプローチになるのかなと思います。

ただ、生成速度は早いので、繰り返し試行錯誤していくことで解決できました。

作成例をちょっとお見せします。最初は攻撃のヒット音ですね。これは "Flash impact hit sound, punchy and heavy" というプロンプトで生成したものです。

次のは魔法攻撃がヒットした時の音ですね。本当はもっと神秘的な感じにしようかと思ったんですが、それだとダメージの痛みが伝わらないなと思って、最終的にかなりシンプルな破裂音にしました。
-->

---
layout: image-right
image: /mh-audio-tailor.png
---

# 効果音の編集

- 生成した音は仕様がランダム
  - 不要な無音部分
  - 音量が様々
  - ループ音に不要なフェードイン・アウト

- 専用のツールを開発
  - github.com/keijiro/AudioTailor
  - 無音部分のトリミング
  - 音量のノーマライズ
  - ループ変換

<!--
生成された効果音は外部ツールを使って若干の編集を施しました。というのも、AI で生成したオーディオクリップは、不要な無音部分を含んでいたり、音量の小さいものが存在するんですよね。これを、オーディオ波形エディタ、例えば Audacity などを使って編集します。

のちに、この作業は簡単に自動化が可能だと思ったので、実際に自動的にこのような加工を行うツールを作りました。それがこの AudioTailor パッケージです。これを使うと、無音部分の削除や音量のノーマライズをボタン一発で行えます。このような未調整の効果音アセットを使用する際には便利なツールだと思いますので、ぜひ活用して下さい。
-->

---
layout: two-cols-video
---

# パーティクルエフェクトの作成

- AI Assistant で Particle System を作成
- シンプルなパーティクルの動きであれば対応可能

::right::

<SlidevVideo muted autoplay loop>
  <source src="/mh-particle-system.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このプロジェクトではパーティクルエフェクトも AI Assistant を使って作成しました。すごく凝った動きとか特殊なエフェクトを作るのは難しいですが、ごく一般的な動きのパーティクルエフェクトであれば、AI Assistant で十分対応可能です。この動画のような典型的なエフェクトであれば、スプライト素材の生成も含めて AI Assistant に作ってもらうことができます。
-->

---
layout: image-right
image: /mh-custom-shader.png
---

# シェーダーの生成

- テキストベースの Unlit シェーダーであれば問題無く生成できる

<!--
シェーダーも AI Assistant で作成しています。テキストベースの、つまり HLSL ベースの Unlit シェーダーであれば、問題無く生成できます。

ここで作成したのは、スプライトを指定した色で塗り潰す、というシェーダーです。標準のスプライトシェーダーは tint color を使って色を掛け合わせることはできるのですが、完全に指定した色で塗り潰すということはできません。そのため、塗り潰し専用のカスタムシェーダーを生成してもらいました。キャラクターがフラッシュする演出なんかで使っています。

このようにライティングを行わない Unlit シェーダーであれば問題無いのですが、ライティングを行う Lit シェーダーでは少し問題が発生します。このことについては次のプロジェクトで詳しく触れます。
-->

---

<div class="h-full flex flex-col">

# スタイルについて

- 今回は KinoEight エフェクトは使用しなかった。
- 特殊なエフェクトに頼らずにスタイルの統合が実現できるか確かめたかったため。
- ある程度実現できたと思うが「AI 臭さ」は少し強まった気がする。

<img src="/mh-game-over.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
ちなみに少し余談になるのですが、このプロジェクトでは、前に解説した KinoEight エフェクトを敢えて使用しませんでした。そういった特殊なエフェクトに頼らずに、アートスタイルの統合感を出せるかどうか確かめたかったためです。

実際に、丁寧にイメージボードなどを用意することで、ある程度の統合感は実現できたと考えています。ただしその反面、ある種の「AI 臭さ」というか…… Nano Banana を使ったことのある方なら分かるかもしれませんが、これって Nano Banana っぽいな、と感じさせるクセというか雰囲気というか、そういうのがあるんですよね。これについては、エフェクトを外したことや、制御しやすいスタイルに統一していったことによって、少し強まってしまっている気がします。

この辺りをどうバランスしていくか、というのは、今後の課題になっています。
-->

---
layout: section
---

# その他のAI Assistantの使用

<!--
最後に、その他のちょっと変わった AI Assistant の使用方法について触れたいと思います。
-->

---
layout: image-right
image: /mh-game-balance-tool.png
---

# ゲームバランス調整ツール

- パラメーターの変更による難易度の変化を確認するツール
- 関連するパラメーターを単一の Scriptable Object に集約
- そのカスタムエディタとして UI を構築

<!--
このプロジェクトでは、最初にマッチ３パズル部分を作ってから、そこに RPG 的な要素を追加していったわけですが、その RPG 部分のゲームバランスを調整するにあたって、専用のツールを AI Assistant に作ってもらいました。

これはゲーム内のパラメーター、例えばレベルアップに必要な経験値や、レベルアップで増加するヒットポイントの量とかですね、そういったものを変更すると、その結果として難易度がどのように変化するのか、シミュレートして表示してくれるツールです。RPG 的な成長要素のあるゲームは、ちょっとした数値の変更で手応えが大きく変化するので、この手のツールを用意することはとても重要になると思います。

実装は簡単で、ゲームバランスに関連するパラメーターを単一の ScriptableObject に集約したうえで、そのカスタムエディタとしてこのような UI を構築するように指示しました。

このようなゲームデザインの補助ツールを即席で作れるのは AI assisted なゲーム開発の利点だと思いますし、エンジニア以外の方々が自分の作業を自分のアイデアによって、自力で効率化することができる、というのは、開発体験の向上に大きく寄与できるものだと思います。
-->

---
layout: section
---

# まとめ

<!--
最後にこのプロジェクトのまとめです。
-->

---

# プロジェクトの振り返り

- 「Unity AI でゲームは開発できる」という手応え

- （この時点での）Unity Lite の制約の認識
  - コンテキストが埋まりやすかった
  - 持続性の高いタスクの実行が難しかった

<div class="flex items-center justify-center gap-3 mt-8">
  <img src="/mh-context-window.png" class="w-60 rounded" />
</div>

<!--
最後にまとめですが、このプロジェクトを通して、ゲームのプロトタイプやカジュアルゲームなら Unity AI と Unity Lite の組み合わせで十分に開発できるという手応えが得られました。

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

# ゲーム概要

- 「ドリフトをきめながらマシンガンで敵を蜂の巣にしたらカッコいいのではないか」
- アイデア検証用のプロトタイプ
- ゲームとして必要最低限の内容

::right::

<SlidevVideo muted autoplay loop print-timestamp="3">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このゲームは「ドリフトをきめながらマシンガンで敵を蜂の巣にしたらカッコいいのではないか」というアイデアを思いついて、それを検証するためだけに作った、プロトタイプ的なプロジェクトです。まさにこのアイデアを検証するために必要な部分だけしか実装されていません。敵も一種類しか存在しませんし、プレイヤー側の操作も最低限のものしか実装されていません。

それでも実際に作ってみることで、これは楽しくてカッコいいし、ゲームとして面白苦なりそうだ、という手応えをちゃんと得ることができました。
-->

---

<div class="h-full flex flex-col">

# 開発背景

- Unity Default を使用
- 3D ゲームの開発に挑戦
  - Tripo P1 の評価
- 短期間での開発（実質３日間）

<div class="flex-1 min-h-0 flex items-center justify-center">
  <img src="/dm-buggy-design.png" class="rounded w-80" />
</div>

</div>

<!--
このプロジェクトでは初めて Unity Default モデルを使用しています。

また、このプロジェクトでは初めて 3D ゲームの開発に挑戦しています。これはまた後で解説しますが、3D モデル生成用の Generator として Tripo P1 が使えるようになったので、これを試したかったというのが動機としてあります。

このプロジェクトは最短期間で検証を済ませたかったので、制作期間はかなり短いです。実質的に３日間ぐらいの作業で済ませています。
-->

---
layout: section
---

# 開発の流れ

<!--
次に開発の流れについてですが、基本的な考えは前のプロジェクトと変わりません。ここでは、このプロジェクトで初めて取り組んだ要素や、このプロジェクトならではのユニークな要素について、かいつまんで解説していきます。
-->

---
layout: two-cols-video
---

# 無限地形生成システム

- 「無限の荒野」を自動生成  

<blockquote>

次に地面を無限生成するシステムを構築します。適当な範囲（10mx10mとか）を１セグメントとして扱い、それを16x16とかの適当な解像度のグリッドとします。

..

このグリッドは適当なフラクタルノイズ関数を使って自然な凹凸を与えます。そして、自車が存在するセグメントの周囲のセグメントについて動的に生成を行っていくことで、無限に走っても地面が続くようにします。このとき、セグメント間に継ぎ目ができないように気をつけて下さい。このような無限地面システムの実装プランを立てて下さい。
</blockquote>

::right::

<SlidevVideo muted autoplay loop>
  <source src="/dm-ground-generation.mp4" type="video/mp4" />
</SlidevVideo>

<!--
まず最初にプロシージャルな無限地形生成システムを作ってもらいました。荒野を走り回りながら敵を次々に倒していく、という内容にしたかったので、それに必要な荒野の地形を自動的に生成できるようにしたわけです。

プロンプトはこんな感じで、Plan Mode でプランを立ててから、それを実行しました。

これについては特に問題無く一発で実装できました。あとはパラメーターをいくつか増やしたりというような調整を行っただけです。
-->

---
layout: two-cols-video
---

# 地形用シェーダー

- 頂点カラーを適用する URP Lit シェーダが必要に 
- URP Lit シェーダーを実装するのは難しい
  - 大量のボイラープレート
  - バージョン毎の細かな差異
- Unity Default では難しかった

::right::

<SlidevVideo muted autoplay loop>
  <source src="/dm-wrong-shader.mp4" type="video/mp4" />
</SlidevVideo>

<!--
今回はローポリ風の絵作りを目指していたので、最初は地面に何もテクスチャを貼らずに動かしていました。ただそれだと、移動したときのスピード感が得られにくいという問題が発生しました。そこで、頂点カラーを使った簡単なチェッカー模様を付けることにしました。

ここで問題となったのが、頂点カラーを適用するカスタムシェーダーの作成です。この地面には陰影を付けたり影を落としたりしたいので、URP Lit シェーダーにする必要があります。

僕は、これは AI にはかなり難しいのではないかと踏んでいました。というのも、URP の各種機能と互換性を保つには、シェーダーに大量のボイラープレート的なコードを組み込む必要があります。また、バージョンによる細かな違いも存在しています。それらを守って正しく実装するのは、実はかなり難しいんですよね。

いちど試しに Unity Default モデルに URP Lit シェーダーの生成に挑戦してもらったのですが、影が落ちなかったり、思ったように色が付かなかったりと、不具合が連発したので止めておきました。

この動画は失敗したシェーダーの例ですが、妙なシームが現れてしまっていますよね。恐らくシャドウのカスケードの境界がおかしくなっているのだと思います。
-->

---
layout: image-right
image: /dm-shader-graph.png
---

# 地形用シェーダー

- 簡単な Shader Graph を手動で作成

<!--
今回は、実現したいことは非常に簡単な内容だったため、ここで無理はせず、Shader Graph を手動で作成することで解決しました。たったこれだけのシェーダーですね。

このように僕の場合はシェーダーの内容が簡単だったので手作業で回避できましたが、複雑なシェーダーを AI に作ってもらいたい、という場合はどのようにすれば良いでしょうか？ 実は Unity 6.5 以降であれば手軽な解決方法があります。
-->

---

<div class="h-full flex flex-col">

# Shader Function Reflection API

- HLSL シェーダーをカスタムノード化
- Unity 6.5 以降で使用可能

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

# 車の挙動の作り込み

- 最初のプロトタイプは擬似物理による挙動になっていた

<blockquote>
🤖 現在の実装は単一の Rigidbody に直接力を加える「疑似物理（アーケードスタイル）」で構築されています。
</blockquote>

<blockquote>
🤖 オフロードゲームを開発するにあたり、Unityの WheelCollider を使用すべきかどうかは非常に重要な設計上の分岐点となります。結論から申し上げますと、このプロジェクトにおいては、現在の「単一 Rigidbody による疑似物理」アプローチの方が圧倒的におすすめです。
</blockquote>

- 敢えて物理挙動を使うよう指示

::right::

<SlidevVideo muted autoplay loop>
  <source src="/dm-physics-arcade-style.mp4" type="video/mp4" />
</SlidevVideo>

<!--
さて、次に車の挙動の作り込みを行いました。実は、AI エージェントは最初のプロトタイプとして、擬似物理、いわゆるアーケードスタイルの挙動を実装してきたんですよね。車輪のシミュレーションを行わず、単一の rigid body で擬似的に車の動きを表現する、というものです。

これは実際に賢い選択で、今回のようにリアリティを重視しない内容で、非現実的なドリフト挙動などがコンセプトに盛り込まれている場合、理にかなっている判断だと思います。一般論で言えば、擬似物理の方が制御の自由度が高くて、調整もしやすいはずなんですよね。

ただ、擬似物理を選択したことによって、車輪のサスペンションがまったく効かず、地面の凹凸に引っ掛かりやすい挙動になってしまっていました。また、僕としては、こういったゲームで物理挙動を使った場合の破天荒な動きにも、また面白さや遊びの余地があると考えていましt。

そこで、ここでは敢えてリアルな物理挙動を使ってほしいと AI エージェントに指示して、作り直してもらうことにしました。

こういった感じで、AI が理にかなった選択をしてくれるんだけど、現実問題としてそれじゃダメなんだよなー、と感じることが時折あります。この物理挙動の問題は、このプロジェクトにおける象徴的な出来事でした。
-->

---
layout: video
video: /dm-drift-prototype.mp4
---

# ドリフト挙動の初期実装

<!--
次に、このプロジェクトのコアとなる、ドリフトの挙動を実装することになります。ロックオンした敵の方を向きながらスライドしていくような挙動を組むわけですね。まずは何も指示せずにエージェント任せで作ってみてもらったのですが、こんな感じになりました。まあ一応それっぽい挙動になってはいるんですが、敵にロックオンしている感じがちょっと弱いかなと思います。もっと力強くスライドしながら、それでも敵を狙い続ける、というような激しさが欲しいと思いました。
-->

---
layout: video
video: /dm-drift-rework.mp4
---

# ドリフト挙動の改良

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

# Unity Default の効果

- コンテキストの作り直しは基本的に無し
- 過去のプロジェクトと比較して作業の持続性が向上

<!--
さて、ここまでの作業で Unity Default モデルを使用した感想を簡単にまとめておきます。以前のプロジェクトではタスク毎にコンテキストを新規作成するような使い方が多かったですが、このプロジェクトでは基本的にコンテキストを作り直すことなく作業を続けることができました。毎日、最初にコンテキストを作成したら、その上で一日作業を続ける、という感じですね。過去のプロジェクトと比較して、持続した作業を行うことが容易になったと感じます。

また、基本的な推論能力もかなり向上していると感じました。これについては定量的な比較を行っていないので、あくまでも感覚的な話になってしまうのですが、指示した内容を正しく汲んで、正しい作業を行ってくれていると言う感覚があります。もちろん、先ほども触れたように、その判断を敢えて変える必要もあったわけですが、その判断に至るまでの道筋はちゃんと正しく実行してくれている、と言う感じです。
-->

---
layout: section
---

# アセット制作の流れ

<!--
次に Drift Mayhem におけるアセット制作の流れについて、前のプロジェクトと異なる点のみ触れたいと思います。
-->

---
layout: image-right
image: /dm-tripo-generation.png
---

# 3D モデル生成

- Tripo P1 を使用
- トライアングル数を制御可能
- 綺麗なトポロジー
- glTF バイナリ形式 (.glb)
  - glTFast パッケージを使用
  - 埋め込みテクスチャ対応

<!--
このプロジェクトでは 3D モデルの生成に Tripo P1 モデルを使用しました。このプロジェクトを開始する少し前に使用可能になったので、早速試してみたというわけです。

Tripo P1 は他の汎用的な 3D 生成モデルと比較して、ゲーム開発に最適化された特性をいくつも備えています。トライアングル数に上限を設けることができますし、比較的綺麗なトポロジーのメッシュを生成することができます。

出力形式としては glTF のバイナリ形式である .glb 形式を使用し、Unity 側では glTFast パッケージを使用してインポートしています。.glb 形式を使うのは、テクスチャデータをファイル内に埋め込むことができるからですね。これによって、Tripo P1 からテクスチャとマテリアルまで含めて単一の .glb ファイルとして出力することができます。
-->

---
layout: image-right
image: /dm-model-generation.png
---

# 3D モデル生成の流れ

- イメージボードを作成
- パーツ毎に分割
- パーツ毎にモデルを生成

<!--
Tripo P1 は入力画像を必要とするので、まず最初にイメージボードを作成します。これには普通のスプライトと同じように Gemini や Nano Banana などの画像生成モデルを使います。

次にパーツへの分解を行います。この車体は屋根に砲塔があるのと、あとはタイヤをそれぞれ独立して回転させる必要があるので、これらのパーツを独立した画像に分割します。この分割にも Nano Banana などの編集機能のある画像生成モデルを使います。

最後に、それぞれのモデルを Tripo P1 で生成します。
-->

---
layout: image-right
image: /dm-glb-embedded-texture.png
---

# 埋め込みテクスチャの問題

- .glb 埋め込みテクスチャに注意
  - 高解像度の非圧縮テクスチャになる
  - 設定は変更できない

<!--
こうして生成された .glb ファイルを Unity で使用する際に、注意すべき点がひとつあります。それは、埋め込まれたテクスチャが、高解像度の非圧縮テクスチャになってしまうということです。１枚で何十 MB も消費するテクスチャになってしまうんですね。例えばこの車体のテクスチャであれば、カラーだけで 21.3MB も使っています。

これはメモリを余計に消費するというだけでなく、配布するアプリのサイズも大きくなってしまいます。特に Web ブラウザゲームではアプリサイズを気にしますから、このデメリットは受け入れ難いものがあります。

そして困ったことに、これらの設定はインポート時に変更することができません。glTF の考え方としては、こういうのはエクスポート時に適切に設定しておくべき、と言う感じなんですね。
-->

---
layout: image-right
image: /dm-glb-embedded-texture-tweaked.png
---

# glTFast Tweaks

- 設定を上書きするツールを作成した
- github.com/keijiro/glTFastTweaks

<!--
そこで、このインポート設定をオーバーライドするためのツールを作成しました。glTFast Tweaks という名前のパッケージです。このツールは glTFast のアドオンとして動作して、テクスチャのインポートの際にその設定を書き換えることができます。これで画像サイズを縮小したり、テクスチャ圧縮を有効化したりできます。

例えばこの車体のテクスチャであれば、21.3MB あったのを、リサイズとテクスチャ圧縮によって 0.7MB まで減らすことができました。

この他にも解決のアプローチはあると思いますが、簡易的にはこのようなソリューションを使うことをお勧めします。
-->

---
layout: two-cols
---

# 音楽 (BGM)

- 音楽生成モデル Lyria 3
- 音楽として破綻していないものを生成可能
- ゲーム開始時のジングルに使用

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
---

# まとめ

<!--
最後にこのプロジェクトのまとめを述べておきたいと思います。
-->

---
layout: image-right
image: /dm-hello-unity-default.png
---

# 実用性の向上

- Agent: Unity Default
- 3D Model: Tripo P1
- Music: Lyria 3

<!--
この Drift Mayhem プロジェクトでは、過去のプロジェクトよりも進化した新しいモデル群を使用することができました。主なところでは、Unity Default モデル、Tripo P1 モデル、Lyria 3 モデル、などですね。

対話型の開発アプローチにおいて Unity Default は十分な性能を提供してくれましたし、Tripo P1 はゲームに使いやすいスペックの 3D モデルを生成してくれました。これらのモデルを活用することで、3D アセットを活用するようなタイプのゲームにおいても、効率良くプロトタイピングを行うことができるようになったと思います。
-->

---
layout: image-right
image: /dm-dirty-code.png
---

# コードの劣化

- 実装作業優先で整理整頓は後回しにした
- リファクタリングは全く行わなかった
- その結果コードはかなり劣化した
  - 古い仕様の残骸が多数存在する
  - 名前と機能が一致しない
  - etc...

<!--
その反面、今回は短期間でリファクタリングを行うことなくコーディング作業を重ねていったので、コードの劣化が無視できないレベルになってしまったと感じています。一応、動くコードにはなっているのですが、実態としてはとても汚い状態になっています。クラスやメソッドの機能が名前と一致していなかったり、重複する機能の実装が複数存在していたり、使用していない機能や古い仕様の残骸が残っていたり、等々です。

例えば、このプロジェクトでは敵のオブジェクトを表す言葉として "Target", "Dummy", "Enemy", "Drone" という単語が混在しています。それぞれが何を意味するのか整理しないまま、仕様の追加を重ねていったので、実態が分かりにくくなっています。コードとしては非常に危険な状態ですね。

これらの劣化したコードは、ここから更に開発を続けるならば、整理を行う必要があります。というのも、コーディングエージェントも結局は人間と同じように、クラス名やメソッド名、コメントやドキュメントなどを手掛かりに開発を進めていくので、そこに混乱があれば、AI もまた混乱してしまいます。結局は、人間の読みやすいコードであることが AI にとっても重要である、ということですね。
-->

---
layout: image-right
image: /dm-dirty-code2.png
---

# Unity 開発プラクティスの欠落

- オブジェクトプール未使用
- Rigid Body を多数使用したエフェクト

<!--
また、Unity の使い方としても、一般的な開発プラクティスを疎かにした状態になってしまっています。例えば、弾丸はオブジェクトプールを使用せずに毎回使い捨てになっています。

また、例えばこの火花のエフェクトは Particle System ではなく、このキューブ一つ一つが Game Object になっていて、それぞれに Mesh Filter と Mesh Renderer と Rigid Body が付与されています。ものすごく贅沢な作り方というか……こういう作り方をしてはいけない、とよく言われることを、そのままやってしまっていますよね。

この辺りも、ここから先へ開発を進めていこうとするならば、必ず改善しておかなければいけないポイントになるでしょう。
-->

---

# リファクタリングの重要性

- 指示すればちゃんと改善できる。
- 立ち止まる余地なく実装を続けると劣化しがち。
- 本格的な開発を続けるならば意識的なリファクタリングが必要。

<!--
もちろん AI エージェントは、これがよくない状態であることを知っていて、改善方法も正しく把握しています。改善して下さいと指示すれば、問題なく改善作業を行ってくれます。ただ、そう伝えない限りは、人間から与えられた実装作業の方を優先する、という感じですね。なので、あれを作って下さい、これを作って下さい、と次々に指示を続けていると、自主的にリファクタリングするのはなかなか難しいようです。

Unity を使用してきたユーザーの皆さんだったら、こういった危険な状態を察知することはできると思うのですが、例えば Unity AI から初めて Unity を触る、というような場合には、ここは落とし穴になるかもしれないなと思いました。

エージェントに対して定期的に設計のチェックやリファクタリングを行うよう指示するなど、対策を講じていく必要があるかもしれません。
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

# プロジェクトについて

- 技術デモ
- 3D モデルを任意の平面で切断する機能
- インタラクティブデモ

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4" print-timestamp="3">
  <source src="/ms-demo-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
今までのプロジェクトはゲームをテーマとしてきましたが、最後のこれだけは純粋に技術的なデモです。3D メッシュオブジェクトを任意の平面で切断すると言う機能を実装しました。また、そのインタラクティブ・デモとして、マウス操作で物理オブジェクトを切り刻める、と言うものを作ってみました。
-->

---

<div class="h-full flex flex-col">

# 開発背景

- MCP Server と外部エージェントを使った長時間実行タスクのテスト

<div class="flex-1 min-h-0 flex items-center justify-center">
  <svg width="570" height="190" viewBox="-120 0 570 190" fill="none" stroke="currentColor" stroke-width="2">
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
    <text x="385" y="78" text-anchor="middle" dominant-baseline="central" style="font-size:17px" stroke="none" fill="currentColor">数十分</text>
    <text x="385" y="100" text-anchor="middle" dominant-baseline="central" style="font-size:17px" stroke="none" fill="currentColor">〜</text>
    <text x="385" y="122" text-anchor="middle" dominant-baseline="central" style="font-size:17px" stroke="none" fill="currentColor">数時間</text>
  </svg>
</div>

</div>

<!--
開発背景についてですが、このプロジェクトは MCP Server を利用した長時間タスクの自律実行を試すために立ち上げたものです。

フロンティアモデルを使用した AI 駆動開発においては、数十分とか数時間といった長時間にわたるセッションを人間の手の介在無しに、自律的に実行することがありますが、Unity の AI Assistant は、現状このような用途には特化されていません。

もしこのような開発アプローチを実践したいと思ったら、外部の AI エージェントから MCP を使って Unity Editor と連携する、というのが理想的な組み合わせとなります。それを実際に試してみたというわけですね。
-->

---

# Testability

- 長時間タスクは自動テスト化が必須
- 自動テスト可能な部分を分離して扱う

<!--
そして、このような長時間タスクの自律的実行において必須となるのが testability の確保です。そこで取り組むタスクは自動テストによって検証が可能でなければならない、ということですね。そうでなければ、人間によるチェックが必要になってしまい、そこで自律的実行は止まってしまいます。

このプロジェクトでもインタラクティブ・デモの部分は人間の手による検証が必要なので、そこは分離して考えることにします。
-->

---

# プロジェクトの構成要素

- MeshSlicer クラス
  - Mesh を任意の平面で切断する機能を提供
  - 自動テストを用意
  - Unity MCP Server + Claude Code (Opus 4.8) を使用

- SlicingDemo シーン
  - インタラクティブデモ
  - AI Assistant (Unity Lite) を使用

<!--
以上を前提に、このプロジェクトの構成要素を解説します。まずは MeshSlicer クラスが存在します。これは Mesh の切断機能を提供するものになっており、Test Runner を使用した自動テストが用意されていて、動作検証まで AI エージェントが自律的に行えるようになっています。そしてこの部分は MCP Server と Opus 4.8 を使用して、長時間タスクとして自律的開発を行ってもらいました。

その後に、この機能を使ったインタラクティブデモとして SlicingDemo というシーンと、一連のスクリプト、マウス操作とかを受け取る部分ですね、それを AI Assistant で作成しました。これは比較的シンプルな内容なので Unity Lite を使用しています。
-->

---

# プロンプト

<blockquote>

Unityにおいてメッシュオブジェクトを自由な平面で切断する機能を実装してください。

この機能は、MeshとUnity.Mathematics.Geometry.Planeで表現される平面を与えると、そのMeshを切断してできる２つのMeshを生成して返します。それぞれの切断面には蓋が追加されます。

ソースとなるMeshは、いわゆる2-manifold/watertight条件が満たされている前提とします。 

頂点データは、position, normal, tangent, uv0まで対応します。切断面のuv0は(0,0)に固定とします。

ここではTDD的なアプローチを用いるものとします。すなわち、機能の実装を行う前に網羅的なテストを実装する必要があります。テストの実行にはUnity標準のTest Runnerを使用します。

テストには凸メッシュだけでなく、断面が複数ループ・入れ子（穴あき／アニュラス）になるケースを含めます。具体的にはトーラス、中空パイプ、開いた箱（トレイ状）、ボウル形状を含め、各断面で蓋が正しく閉じることを検証します。また、プロジェクトに含まれているfbxモデルも使用します。

...
</blockquote>

<!--
これが実際に使用したプロンプトですね。ざっくりと大まかに要件を述べつつ、Test Driven Development 的な手法で進めるように指示しています。

まだもうちょっと続きがあります。
-->

---

<blockquote>
...

実装は最初に最適化を考えない形で行います。ここでは正しさを重視し、パフォーマンスは考慮しません。その実装が完成したら、Mesh Rendererを使ってシーン上でのレンダリングも行い、あなた（AIエージェント）の視覚を利用した定性的な検証も行います。

次にパフォーマンスを計測します。ここでは、メソッド単体でのパフォーマンスと、システム総合でのパフォーマンスと、両方を分けて計測します。後者については、適量のハイポリメッシュを毎フレーム切断したうえでMesh Rendererで描画することで、描画まで含めた負荷を測るものとします。

それらが完了したのちに最適化を開始します。ここではBurstコンパイラ、C# Job Systemを使用しつつ、NativeArrayやAdvanced Mesh APIを活用することでなるべく配列コピーを防ぐような工夫を盛り込みます。ここでは前述のパフォーマンス計測方法を使用してその効果を確認します。繰り返し何度か最適化を試み、妥当な成果が得られたところで作業完了とします。

</blockquote>

<!--
続きの部分では開発の流れを指定していますね。まず最初は、パフォーマンスを考えずに正しさを重視したナイーブな実装を行うよう指示しています。そしてそれをベースに最適化を行い、結果を比較するように指示していますね。

つまり、計画、実装、確認、改良、というようなループを自律的に回すよう指示しているわけです。
-->

---

<div class="h-full flex flex-col">

<SlidevVideo muted autoplay controls class="flex-1 min-h-0 w-full object-contain">
  <source src="/ms-long-session.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
これは実際に実行している様子を早回しにしたものです。完了までに約50分費やしています。今どきの長時間タスクでは何時間も自律的に実行するケースがザラにあるので、これはまあ、まだ短い方だと思います。

完了しましたね。ここに結果が提示されています。
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
パフォーマンスの比較表がこちらです。Burst 対応によって 8.8 倍になったと書かれていますね。

このあと、AI Assistant を使ってインタラクティブ・デモの部分を作成したわけですが、その部分については、今までのプロジェクトと大差無いので割愛します。
-->

---
layout: two-cols-video
---

# 不具合の発生と特定

- 特定のアングルで穴が生じる不具合

::right::

<SlidevVideo muted autoplay loop>
  <source src="/ms-corner-cases.mp4" type="video/mp4" />
</SlidevVideo>

<!--
それで、これで完成しました、となればハッピーエンドなのですが、実際にはそう上手くはいきませんでした。一見うまく動いているのですが、たまに切断面に穴が生じるという不具合が発生しました。

これをテストするために切断面を手動で微調整できるテスト用シーンを作ってもらい、不具合の生じる条件を手動で特定しました。そして、その条件を保存したうえで、AI エージェントに原因を特定してもらう、というワークフローですね。
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
調査の結果、切断面に接する頂点やエッジがある場合に、切断面の構築に失敗するケースがあるということが分かりました。この問題に対する解決法も色々と提示されましたが、どれも少し負荷の高いものだったので、代替案として切断面のオフセットによるワークアラウンドを提案しました。このようなエッジケースを検出したら、切断面をずらすことで問題を回避してしまおう、というものですね。

このワークアラウンドは効果てきめんで、その結果、冒頭にお見せしたような安定した動作を得ることができました。
-->

---
layout: section
---

# その他に利用した機能

<!--
次に、このプロジェクトのインタラクティブ・デモの作成でいくつかの Unity AI の機能を利用したので、それについて触れておきたいと思います。
-->

---

<div class="h-full flex flex-col">

# MCP Tools (MCP clients)

- 切断可能なモデルへの変換に Blender を使用
- AI Assistant から MCP 経由で Blender を制御
  - `blender-mcp` を使用

<img src="/ms-mcp-client.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
まず利用したのは MCP Tools の機能です。これは AI Assistant から外部の MCP クライアントを利用するというものです。MCP Server の機能と混同しないように気をつけて下さい。こっちは MCP クライアントを利用する機能ですね。 Unity 内の AI Assistant から外部のツールを、例えばここでは Bldner を、MCP で操作するわけです。

ここでは 3D モデルを、いわゆるマニフォールドモデルとかソリッドモデルとか言われる「切断可能なタイプのモデル」に変換するのに、これを利用しました。AI Assistant から Blender を操作して、Blender 上でその変換を行ってもらうわけです。Unity プロジェクトに含まれる .glb ファイルをロードして、加工して、.glb ファイルとして再エクスポートしてもらう、という感じです。
-->

---

<div class="h-full flex flex-col">

<img src="/ms-mcp-config.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
MCP Tools 設定は Project Settings の中にあります。この "Enable MCP Tools" をオンにしたうえで、ここにある "mcp.json" ファイルに設定を加えます。うまく設定できれば、この "Servers" の所に blender が出現するはずです。
-->

---

<div class="h-full flex flex-col">

# スキル機能

<img src="/ms-skill-config.png" class="flex-1 min-h-0 w-full object-contain mt-4" />

</div>

<!--
また、その Blender 上での操作手順については、AI Assistant のスキル機能を活用することにしました。

スキルというのは、AI エージェントによくある機能ですが、ツールの使い方や定型的な手続きを教えるための仕組みですね。これによって、Blender の機能をどういう風に呼び出せばスライス可能なモデルを作れるか、教え込む事ができるわけです。

このようなプロジェクト毎のスキルは Assets の Skills ディレクトリの中に配置します。

スキル関係の設定は Preference の中にあります。ここに作成したプロジェクトスキルが表示されるはずです。デフォルトでは "Deny" になっているので "Allow" に変更しましょう。

このように MCP Tools とスキルの組み合わせによって、マニフォールドモデル変換が完全に自動化されました。AI Assistant に「このモデルをスライス可能にして」と命令すれば、あとは勝手に Blender を呼び出して変換してくれるわけですね。

このように、AI Assistant の MCP Client 機能とスキル機能は、外部アプリやサービスとの連携を自動化するにあたって便利な機能ですので、そのような要素がある場合にはぜひ活用してください。
-->

---

# まとめ

- MCP Server は外部エージェントを使用した長時間タスクの実行に便利
- MCP Client 及びスキル機能は外部ツールとの連携に便利

<!--
まとめです。このように、MCP Server を使用することによって、外部エージェントを使った長時間タスクの実行が可能になります。最近は Unity AI でもフロンティアグレードのモデルが使えるので、必ずしも外部のエージェントを使わなくてはならないという訳ではないですが、長時間タスクの実行や開発ループの構築に関しては、やはりメジャーなエージェントにコミュニティの知見が蓄積されていますので、そちらを使うメリットが大きいのかなと思いました。

また、MCP Client 機能については、Unity AI Assistant から外部ツールを操作するのに使えることが分かりましたし、その手続きを整理するのにカスタムスキル機能が便利であることも確認できました。
-->

---

<img src="/unite-thankyou-bg.jpg" class="absolute inset-0 w-full h-full object-cover" style="transform: scaleY(-1)" />

<div class="absolute flex items-center" style="left:7%; top:21.9%; width:30.9%; height:56.4%">
  <h1 style="font-size:49px; line-height:1.25">Thank you</h1>
</div>

<div class="absolute bg-white" style="left:54%; top:26.8%; width:26%; height:46.2%"></div>
