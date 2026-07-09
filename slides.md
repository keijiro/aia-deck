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
  sans: PT Serif
  provider: google
---

# Developing with Unity AI: Practical Use Cases

## Keijiro Takahashi

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

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Mirror Mage

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4">
  <source src="/mm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
まず最初のこのプロジェクトは "Mirror Mage" というカジュアルゲームです。敵の攻撃を反射して、それを攻撃に使う、というちょっと変わったシステムのアクションゲームです。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Dungeon Match Heroes

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4">
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
次のプロジェクトは "Dungeon Match Heroes" というカジュアルゲームです。マッチ３パズルゲームに RPG のエッセンスを加えたようなゲームですね。
-->

---

<SlidevVideo autoplay autoreset="slide" :muted="$renderContext !== 'slide'" class="absolute inset-0 w-full h-full object-cover">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

---

<div class="h-full flex flex-col">

# Drift Mayhem

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4">
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
３つ目は "Drift Mayhem" という、オフロードカー・シミュレーションとシューティングが融合したようなゲームのプロトタイプですね。
-->

---

<div class="h-full flex flex-col">

# Mesh Slicer

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4">
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
layout: cover
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

<SlidevVideo muted autoplay loop>
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

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4">
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
    <DensityTile :n="11" :palette="['#c0392b', '#27ae60', '#2980b9', '#8e44ad', '#f39c12', '#16a085', '#e67e22', '#2c3e50']" />
    <DensityTile :n="8" :palette="['#e74c3c', '#3498db', '#f1c40f', '#9b59b6', '#1abc9c', '#e67e22']" />
    <DensityTile :n="6" :palette="['#2980b9', '#e67e22']" :seed="42" />
  </div>
</div>

<div class="relative flex items-center justify-center h-26 opacity-70">
  <svg width="28" height="104" viewBox="0 0 28 104">
    <line x1="14" y1="2" x2="14" y2="95" stroke="currentColor" stroke-width="2" />
    <path d="M9 93 L14 102 L19 93 Z" fill="currentColor" stroke="none" />
  </svg>
  <div class="absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 px-4 py-1 text-sm border rounded bg-white dark:bg-[#121212]" style="border-color: currentColor;">filtering</div>
</div>

<div class="flex flex-col items-center gap-2">
  <div class="flex gap-4 items-center">
    <DensityTile :n="6" :palette="['#2980b9', '#e67e22']" />
    <DensityTile :n="6" :palette="['#2980b9', '#e67e22']" />
    <DensityTile :n="6" :palette="['#2980b9', '#e67e22']" :seed="42" />
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
layout: cover
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

<SlidevVideo muted autoplay loop>
  <source src="/mh-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このプロジェクトはマッチ３パズルに RPG 的なエッセンスを付け加えたようなカジュアルゲームです。このグリッドは、一番下の段だけがインタラクション可能で、クリックすることでブロックを壊せます。これを壊してブロックを３つ以上並べることで、それぞれのブロックが持つ効果を引き出すことができる、というシステムです。

RPG 的な成長要素があって、経験値を貯めることでレベルアップします。経験値は敵を倒すだけでなく、鍵を使って宝箱を開けたり、多くのブロックをいっぺんに消したりすることで稼げます。敵は徐々に強くなっていくので、そうやってうまく経験値を稼いでいかないと、段々とプレイが難しくなっていく、という内容になっています。
-->

---
layout: image-right
image: /mh-heroes.png
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
- 約 10 日間で制作

- C# スクリプト、シェーダー、スプライト、アニメーション（スプライトシート）、効果音を Generator で生成
- Unity Editor の操作もなるべく AI Assistant に任せるようにした

<!--
まだこの段階でも、Unity Lite モデルしか存在していませんでしたので、Unity Lite を全ての作業に使用しました。また、各種のアセットも Generator で生成し、Unity Editor の操作もなるべく AI Assistant 任せにしました。この辺りは前作と同じですね。
-->

---
layout: section
---

# 開発作業例

ここは「Unity 自習室」から引用する

---
layout: section
---

# アセット制作の流れ

<!--
さて、ここから少し、Generator を使ったアセットの作成方法について触れたいと思います。
-->

---
layout: image-right
image: /mh-generator-models.png
---

# 使用モデル

- 様々なモデルが使用可能
- 画像生成は Gemini 3.0 Pro, Gemini 3.1 Nano Banana 2 の使用頻度が高い

<!--
Generator には様々な生成モデルがカタログ的に並べられていて、用途に合わせて使い分けることができるようになっています。ただ、色んな事情があって、使用するモデルは一部に絞られてくると思います。

例えば、画像生成であれば、Gemini 3.0 Pro, Gemini 3.1 Nano Banana 2 を使う機会が圧倒的に多いかなと思います。というのも、ローカル言語、つまり韓国語や日本語を問題無く使うことのできる画像生成モデルって、この辺りに限られてくるんですよね。それに加えて、表現力の高さや編集能力の高さを考慮すると、これらのモデルを選ばざるを得ない、という感じになります。
-->

---
layout: image-right
image: /mh-image-board.png
---

# イメージボードの作成

- １枚の画像でイメージを固める
  - バラバラの画像で統一したイメージを保つのは難しいため

<!--
そしてまず最初に行うのはイメージボードの作成ですね。これは、キャラクターなどをバラバラに作成すると、スタイルや方向性が散逸してしまうので、１枚の絵の中に収めて生成することで、ベースとなる統一されたイメージを固める、というものです。

このイメージボードにどこまでの情報を含めるかは、プロジェクトの方針次第になると思いますが、今回はここにプレイヤーパーティーのキャラクターだけを含めることにしました。
-->

---

# 各キャラクタの生成

- 単体のキャラクターの切り出し
- Kling を使ってスプライトシートを生成
  - 試行錯誤にかなりの時間が必要とされる
- 背景透過モデルを適用
  - 半透明表現は難しいので避ける

<!--
次に、イメージボードから各キャラクターを切り出します。ちなみに、僕はこの切り出し作業にも Nano Banana を使いました。問題無くできましたが、正直なところ、Photoshop などを使用した方がいいと思います。敢えて試してみたというだけです。

次に、これらのベースとなるスプライトからスプライトシートを生成します。これには Kling などの動画生成モデルを使用することになります。Generator 側では、生成された動画を 16 個のフレームをサンプリングしてスプライトシートにベイクします。

ただ、これらの動画生成モデルを使ったことのある方なら分かると思うんですが、使用にはかなりのコツが必要です。思った通りの動きを作るのはなかなか難しいと思いますし、生成にも時間がかかるので、試行錯誤にはかなり根気が必要となります。恐らく、想像以上に時間とクレジットを消費することになると思いますので、注意してください。

そして最後に背景透過のモデルを適用して完成です。この背景透過モデルもちょっとクセがあるので、使い方のコツを覚えるまで試行錯誤が必要になるかもしれません。特に半透明の表現を扱うことは難しいので、このゲームでもスプライトシートに半透明の魔法の表現を入れることは避けています。
-->

---

# UI 部品の生成

- スプライトと同様
  - Gemini 系モデルで日本語プロンプトで生成
  - 各要素を切り出し
  - 背景透過モデルを適用

<!--
ブロックのパーツや UI 要素についても同じようなワークフローで作成しました。見た目を統一したい部分については１枚の画像に収めて生成して、各要素を切り出してから、背景透過モデルを適用する、という流れですね。
-->

---

# 効果音の生成

- ElevenLabs SFX を使用
- ローカル言語非対応（英語必須）
  - ニュアンスを伝えるのが難しい（言語の壁？）
- 生成は早いので試行錯誤で解決可能
- 実際の生成例

<!--
次に効果音を生成します。今のところ Generator で提供しているモデルの中で効果音を生成できるのは ElevenLabs SFX モデルだけですので、これを使うことになります。

このモデルでは韓国語や日本語を使うことはできませんので、英語を使用する必要があります。しかも、効果音を自然言語を使って表現するというのは、思った以上に難しいと感じました。長く詳細なプロンプトを書いてもニュアンスが伝わらないことが多く、短く端的に伝わる表現をボキャブラリとして覚えておいて、その組み合わせでなんとかする、というようなアプローチになるのかなと思います。

ただ、生成にかかる時間はかなり短いので、繰り返しを重ねて試行錯誤していくことで解決できました。
-->

---
layout: image-right
image: /mh-audio-tailor.png
---

# 効果音の調整

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
生成された効果音は外部ツールを使って若干の編集を施しました。というのも、AI で生成したオーディオクリップは、不要な無音部分を含んでいたり、音量の小さいものが存在するんですよね。これを、オーディオ波形エディタ、僕の場合は Audacity を使って編集しました。

のちに、この作業は簡単に自動化が可能だと思ったので、実際に自動的にこのような加工を行うツールを作りました。それがこの AudioTailor パッケージです。これを使うと、無音部分の削除や音量のノーマライズをボタン一発で行えます。

また、AI Assistant から呼べるように tool 登録やカスタム skill も用意していますので、AI Assistant に「このクリップを整えて」と言えば自動的に処理してくれます。
-->

---

# 余談：エージェント経由での生成

- Generator UI ではなく AI Assistant に生成をさせることも可能。
- 利点
  - プロンプトの作り込みを自動化できる
  - 大量生成を自動化できる

- 欠点
  - プロンプト構築はそこまで上手くない
  - モデルの特性を正しく把握しているわけではない

- プロジェクト毎の skill を定義することで改善できるのではないか

<!--
ここで少し余談になるのですが、このような Generator を使ったアセットの生成は、Generator の UI を直接使うだけでなく、AI Assistant を通して行うことも可能です。AI Assistant に、これこれこういうアセットを作って、と依頼すると、AI Assistant が自動的に Generator を呼び出して生成してくれるわけです。

AI Assistant に任せるメリットはいくつかあります。プロンプトの作り込みを自動化できる、とか、バリエーションを増やしたい場合などにその作業を自動化できる、とか、色々考えられますね。

ただし、実際には、このアプローチはそこまで使いやすくはないなと感じました。というのも、AI Assistant はそこまでプロンプトの構築が上手いわけではなく、余計な表現を増やしてしまいがちな傾向にあると感じました。また、それぞれのモデルの概要は知っていても、そのクセとか特性を詳しく把握しているわけではないので、的外れな方向に進んでしまうことも多いように感じました。

そのため、僕も最初は AI Assistant 経由でアセット生成を行っていたのですが、最終的には Generator を直接使うことになりました。Generator の特性を一旦把握してしまえば、プロンプトを構築するためのルールを決めた上で、それを skill 化することでうまく運用できるのでは無いかと思います。AI Assistant を使った生成ワークフローを構築する場合は参考にしてみてください。
-->

---
layout: two-cols-video
---

# パーティクルエフェクトの生成

- AI Assistant で Particle System の作成が可能
- ごく一般的なパーティクルの動きであれば対応可能

::right::

<SlidevVideo muted autoplay loop>
  <source src="/mh-particle-system.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このプロジェクトではパーティクルエフェクトも AI Assistant を使って作成しました。すごく凝った動きとか特殊なエフェクトを作るのは難しいのですが、ごく一般的な動きのパーティクルエフェクトであれば、AI Assistant で十分対応可能です。ここに貼ってある GIF のようなものであれば全然作れる、ということですね。
-->

---
layout: image-right
image: /mh-custom-shader.png
---

# シェーダーの生成

- テキストベースの Unlit シェーダーであれば問題無く生成できる

<!--
シェーダーも AI Assistant で作成しています。テキストベースの、つまり HLSL ベースの Unlit シェーダーであれば、問題無く生成できます。

ここで作成したのは、スプライトを指定した色で塗り潰す、というシェーダーですね。標準のスプライトシェーダーは tint color を使って色を掛け合わせることはできるのですが、完全に指定した色で塗り潰すということはできないので、そのためのシェーダーを用意してもらいました。キャラクターがフラッシュする演出なんかで使っています。

ただ残念ながら、AI Assistant のシェーダー対応はそこまで強くないというのが正直なところです。例えば URP の Lit シェーダーを作成することは、不可能というわけではないですが、かなり難しいです。Shader Graph を生成するための仕組みも用意されていないので、Shader Graph を使って対応するというのも難しいです。
-->

---
layout: image-right
image: /mh-game-over.png
---

# 余談

- 今回は KinoEight エフェクトは使用しなかった。
- 特殊なエフェクトに頼らずにスタイルの統合が実現できるかどうか挑戦したかったため。
- ある程度実現できたと思うが、「AI 臭さ」は強まった気がする

<!--
ちなみに少し余談になるのですが、このプロジェクトでは、前に解説した KinoEight エフェクトを敢えて使用しませんでした。そういった特殊なエフェクトに頼らずに、アートスタイルの統合感を出せるかどうか試したかったためです。

実際に、先ほど解説したようなテクニックなどを駆使することで、ある程度の統合感は実現できたと考えています。ただしその反面、ある種の「AI 臭さ」というか…… Nano Banana を使ったことのある方なら分かるかもしれませんが、これって Nano Banana っぽいな、って感じさせるクセというか雰囲気というか、そういうのがあるんですよね。これについては、エフェクトを外したことや、制御しやすい統一スタイルなどを適用していったことにより、強まってしまった気がします。

この辺りをどうバランスしていくか、というのは、個人的にも未解決の問題になっています。
-->

---
layout: section
---

# その他の AI Assistant の使用

<!--
最後に、その他のちょっと変わった AI Assistant の使用方法についても触れたいと思います。
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
これは、ゲームバランスを調整するためのツールを AI Assistant で作成した、というものですね。ゲーム内のパラメーターを変更すると、その結果としてバランスがどのように変化するのか、というのを擬似的に算出して視覚化してくれるツールです。この手の RPG 的な成長要素のあるゲームは、ちょっとした数値の変更で手応えが大きく変化するので、最終的なゲームバランスの調整でとても重宝しました。

具体的には、ゲームの難易度に影響するパラメーターを単一の ScriptableObject に集約して、そのカスタムエディタとしてこのような UI を構築するように指示しました。

このようなゲームデザインの補助を行うためのツールを即席で作れるのは AI Assistant の利点だと思いますし、エンジニア以外の方々が自分の作業を自分のアイデアで、自力で効率化することができる、というのは素晴らしいことだと思います。AI 開発手法を導入する大きなモチベーションの一つですね。
-->

---
layout: section
---

# まとめ

<!--
最後にまとめです。
-->

---

# プロジェクトの振り返り

- 「Unity AI でゲームは開発できる」という手応え
- （この時点での）Unity Lite の制約の認識
  - コンテキストが埋まりやすい
  - 持続性の高いタスクの実行が難しい

- 新しいコンテキストがプロジェクトを把握できるようにするための工夫
  - ProjectOverview 文書の頻繁な更新
  - 実行済みの Plan を文書として再利用

<!--
最後にまとめですが、このプロジェクトを通して、ゲームのプロトタイプやカジュアルゲームなら Unity AI と Unity Lite の組み合わせで十分に開発できるという手応えを得ることができました。

その反面、Unity Lite の制約に気づくこともありました。僕がこのプロジェクトで使用した限りでは、実は推論能力についてはそれほど問題にならなかったのですが、どちらかと言うとコンテキストウィンドウが埋まってしまいやすいと感じることの方が多かったです。作業を続けるうちにコンテキストが埋まってしまって、新しいコンテキストへ移行せざるを得ない、と言うタイミングが度々発生してしまったんですね。

コンテキストを切り替える度に AI はプロジェクトの内容を把握し直す必要があるので、それをどうやってうまく行うか工夫する必要がありました。Unity AI には Project Overview 文書を自動生成する機能があるので、これは比較的こまめに更新を行うようにしました。また、実行済みの Plan 文書を蓄積して、過去の作業履歴として把握できるようにもしていきました。

ただこの辺りの工夫は、AI Assistant 自体の調整や、サブエージェントへの対応、Unity Default モデルの登場によって、あまり気にならなくなったと思います。次のプロジェクトでは一つのコンテキストを使い回す形で長期間の作業を行いましたが、特に問題は生じませんでした。

ですので、この辺りの制約は、こういう時期もあった、ということで、今はそれほど気にしなくて良いと思います。
-->

---
layout: cover
---

<BgVideo src="/dm-pr-hq.mp4" />

# Project: Drift Mayhem

---
layout: two-cols-video
---

# ゲーム概要

- 「ドリフトをきめながらマシンガンで敵を蜂の巣にしたらカッコいいのではないか」
- アイデア検証用のバーティカルスライス
- ゲームとして必要最低限の内容

::right::

<SlidevVideo muted autoplay loop>
  <source src="/dm-pr-hq.mp4" type="video/mp4" />
</SlidevVideo>

<!--
このゲームは「ドリフトをきめながらマシンガンで敵を蜂の巣にしたらカッコいいのではないか」というアイデアを思いついて、それを検証するためだけに作った、いわゆるバーティカルスライス的なプロトタイプです。まさにこのアイデアを検証するための部分だけが実装されていて、敵も一種類しか存在しませんし、プレイヤー側の操作も最低限のものしか実装されていません。

それでも実際に作ってみて、これは楽しくてカッコいいし、ゲームとして面白いかもしれないな、という手応えをちゃんと得ることができました。
-->

---

# 開発背景

- Unity Default を使用
- 3D ゲームの開発に挑戦
  - Tripo P1 の評価
- 短期間での開発（実質３日間）

<!--
このプロジェクトでは初めて Unity Default モデルを使用しています。

また、このプロジェクトでは初めて 3D ゲームの開発に挑戦しています。これは、後でまた解説しますが、3D モデル生成用の Generator として Tripo P1 が使えるようになったので、これを試したかったというのが動機としてあります。

このプロジェクトは最短期間で検証を済ませたかったので、制作期間はかなり短いです。実質的に３日間ぐらいの作業で済ませています。
-->

---
layout: section
---

# 開発の流れ

<!--
このプロジェクトの開発の流れをザクっと解説します。
-->

---
layout: two-cols-video
---

# 無限地形生成システム

- 「無限の荒野」を自動生成  

<br/>

<blockquote>
次に地面を無限生成するシステムを構築します。適当な範囲（10mx10mとか）を１セグメントとして扱い、それを16x16とかの適当な解像度のグリッドとします。<br/>
...<br/>
このグリッドは適当なフラクタルノイズ関数を使って自然な凹凸を与えます。そして、自車が存在するセグメントの周囲のセグメントについて動的に生成を行っていくことで、無限に走っても地面が続くようにします。このとき、セグメント間に継ぎ目ができないように気をつけて下さい。このような無限地面システムの実装プランを立てて下さい。
</blockquote>

::right::

<SlidevVideo muted autoplay loop>
  <source src="/dm-ground-generation.mp4" type="video/mp4" />
</SlidevVideo>

<!--
まず最初にプロシージャルな無限地形生成システムを作ってもらいました。荒野を走り回りながら敵を次々に倒していく、という内容にしたかったので、それに必要な荒野の地形を自動的に生成できるようにしたかったんですよね。

プロンプトはこんな感じで、Plan Mode を使ってプランを立ててから、それを実行しました。

これについては特に問題無く実装できて、あとはパラメーターをいくつか増やしたりという調整を行っただけです。
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
今回はローポリ風の絵作りを目指していたので、最初は地面に何もテクスチャを貼らずに動かしていました。しかし、何らかの模様が地面についていないとスピード感が出にくいというのが分かりました。そこで、頂点カラーを使った簡単なチェッカー模様を付けることにしました。

ここで問題となったのが、頂点カラーを適用するカスタムシェーダーを作成する必要がある、ということです。しかも、この地面には陰影を付けたり影を落としたりしたいので、URP Lit シェーダーにする必要があります。

僕は、これは AI にはかなり難しいのではないかと踏んでいました。というのも、URP の各種機能と互換性を持つには、大量のボイラープレート的なコードを組み込む必要がありますし、バージョンによって微妙に異なる点も多くあります。これらを守って正しく実装するのは、非常に難しいんですよね。  

いちど試しに Unity Default モデルに URP Lit シェーダーの生成に挑戦してもらったのですが、影が落ちなかったり、思ったように色が付かなかったりと、不具合が連発したので止めておきました。

恐らく色々お膳立てすれば生成できなくも無いと思うのですが、コスト対効果は決して良くないでしょう。

今回は、実現したいことは非常に簡単な内容だったため、Shader Graph を手動で作成することで解決しました。
-->

---
layout: image-right
image: /dm-shader-graph.png
---

# 地形用シェーダー

- 簡単な Shader Graph を手動で作成

<!--
今回は、実現したいことは非常に簡単な内容だったため、Shader Graph を手動で作成することで解決しました。
-->

---
layout: image-right
image: /dm-shader-reflection.jpg
---

# もしシェーダー生成をするなら？

- Shader Function Reflection API
  - Unity 6.5 移行で利用可能
  - HLSL シェーダーをカスタムノード化

<!--
複雑なシェーダーをどうしてもAI に書いてもらいたい場合は、Unity 6.5 で導入された Sahder Function Reflection API を使用するのが良いと思います。これは、HLSL シェーダーにコメントとしてリフレクション情報を埋め込む、という仕組みです。これを使うことで、HLSL シェーダー関数が Shader Graph 上のカスタムノードとして利用可能になります。

これを使って、処理の本体は AI に HLSL として書いてもらいつつ、シェーダーの入出力との接続は Shader Graph 上で行う、という役割分担が可能になるわけですね。

将来的には Shader Graph との繋ぎ込みも自動化したいところですが、とりあえず現状ではこのような手段をとることが可能になっています。
-->

---
layout: two-cols-video
---

# 車の挙動の作り込み

- 最初のプロトタイプは擬似物理による挙動になっていた

<br/>

<blockquote>
🤖 現在の実装は単一の Rigidbody に直接力を加える「疑似物理（アーケードスタイル）」で構築されています。
</blockquote>
<br/>
<blockquote>
🤖 オフロードゲームを開発するにあたり、Unityの WheelCollider を使用すべきかどうかは非常に重要な設計上の分岐点となります。結論から申し上げますと、このプロジェクトにおいては、現在の「単一 Rigidbody による疑似物理」アプローチの方が圧倒的におすすめです。
</blockquote>

<br/>

- 敢えて物理挙動を使うよう指示

::right::

<SlidevVideo muted autoplay loop>
  <source src="/dm-physics-arcade-style.mp4" type="video/mp4" />
</SlidevVideo>

<!--
さて、次に車の挙動の作り込みを行いました。実は、AI エージェントは最初のプロトタイプとして、擬似物理、いわゆるアーケードスタイルの挙動を実装してきたんですよね。車輪のシミュレーションを行わず、単一の rigid body で擬似的に車の動きを表現する、というものです。

これは実際に賢い選択で、今回のようにリアリティを重視しない内容で、非現実的なドリフト挙動などがコンセプトに盛り込まれている場合、理にかなっていると思います。一般論で言えば、擬似物理の方が制御の自由度が高くて、調整もしやすいはずなんですよね。

しかし、擬似物理を選択したことによって、車輪のサスペンションがまったく効かず、地面の凹凸に引っ掛かりやすい挙動になってしまっていました。また、僕としては、こういったゲームで物理挙動を使った場合の破天荒な動きにも、また面白さや遊びの余地があることを知っていました。

そこで、ここでは敢えてリアルな物理挙動を使ってほしいと AI エージェントに指示して、作り直してもらうことにしました。

こういった感じで、AI が実に理にかなった選択をしてくれるんだけど、実際の現実問題としてそれじゃダメなんだよなー、と感じることが時折ありますよね。この物理挙動の問題は、このプロジェクトにおける象徴的な出来事でした。
-->

---
layout: video
video: /dm-drift-prototype.mp4
---

# ドリフト挙動の初期実装

<!--
次に、このプロジェクトのコアとなる、ドリフトの挙動を実装することになります。ロックオンした敵の方を向きながらスライドしていくような挙動を組むわけですね。まずは何も指示せずにエージェント任せで作ってみてもらったのですが、こんな感じになりました。一応それっぽい挙動になってはいるのですが、敵にロックオンしている感じがちょっと弱いかなと思います。
-->

---
layout: video
video: /dm-drift-rework.mp4
---

# ドリフト挙動の改良

<!--
そこで次は、明確に指示を出して改良してみることにしました。アイデアとしては、Configurable Joint を使って明確に束縛関係を作ってしまう、というものです。分かりやすく言うと、敵と自分をロープで縛って、グルッとスイングするような動きにしてしまうんですね。

これは制御がしやすい反面、ガッチリと束縛されているような感じが出てしまうので、動きが不自然になりやすいし、AI エージェントもそれを避けるために、この手段は使わなかった、と言う感じですね。でも実際には、調整と演出次第で何とかなるものです。

ここでもやはり、AI エージェントの出してきた理にかなった選択に対して、もっと割り切っていいと人間から指示出しする構図になっていますね。
-->

---
layout: video
video: /dm-drift-finished.mp4
---

# ドリフト挙動の改良

---

# Unity Default の効果

- コンテキストの作り直しは基本的に無し
- 過去のプロジェクトと比較して作業の持続性が向上

<!--
ここまでの作業で Unity Default を使用した感想を簡単にまとめておきます。以前のプロジェクトではタスク毎にコンテキストを新規作成するような使い方が多かったですが、このプロジェクトでは基本的にコンテキストを作り直すことなく作業を続けることができました。毎日、最初にコンテキストを作成したら、その上で一日作業を続ける、という感じですね。過去のプロジェクトと比較して、持続した作業を行うことが容易になったと感じます。

また、推論能力もかなり向上していると思います。これについては定量的な比較を行っていないので、あくまでも感覚的な感想になってしまうのですが、指示した内容を正しく汲んで、正しい作業を行ってくれていると言う感覚があります。もちろん、先ほども触れたように、その判断を敢えて変える必要が生じることもあったわけですが、その判断に至るまでの道筋はちゃんと正しく実行してくれている、と言う感じです。
-->

---
layout: section
---

# アセット制作の流れ

<!--
次に Drift Mayhem におけるアセット制作の流れについて、新しい要素についてのみ触れたいと思います。
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
このプロジェクトでは 3D モデルの生成に Tripo P1 を使用しました。このプロジェクトを開始する少し前に使用可能になったので、早速試してみたと言う格好です。

Tripo P1 は、正直なところ現状において、ゲーム開発に使用できる唯一の現実的なモデルだと思います。トライアングル数に上限を設けることができて、比較的綺麗なトポロジーのメッシュを出力することができます。

出力形式としては glTF のバイナリ形式である .glb 形式を使用し、Unity 側では glTFast パッケージを使用してインポートしています。.glb 形式を選択したのは、テクスチャデータを埋め込むことができるからですね。Tripo P1 からテクスチャとマテリアルまで含めて単一の .glb ファイルとして Unity 側に取り込むことができます。
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
Tripo P1 はソース画像を必要とするので、まずはイメージボードを作成する必要があります。これには Gemini 3.0 Pro や Nano Banana 2 などの画像生成モデルを使います。

次にパーツへの分解を行います。この車体は屋根に砲塔があるのと、あとはタイヤをそれぞれ独立して回転させる必要があるので、これらのパーツをそれぞれ独立した画像に分割します。この分割にも Nano Banana 2 などの編集機能のある画像生成モデルを使います。

最後に、それぞれのモデルを Tripo P1 で生成します。このディテールのモデルだったら、大体何トライアングルぐらいで作れるかな、というのを勘で設定します。
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
こうして生成された .glb ファイルを Unity で使用する際に、注意すべき点がひとつあります。それは、埋め込まれたテクスチャが、高解像度の非圧縮テクスチャになってしまうということです。１枚で何十 MB も消費するテクスチャになってしまうということですね。これはメモリを余計に消費するというだけでなく、配布するアプリのサイズが大きくなってしまいます。Web ブラウザゲームでは特にアプリサイズを気にしますから、このデメリットは受け入れ難いものがありますね。

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
そこで、このインポート設定をオーバーライドするためのツールを作成しました。glTFast Tweaks という名前のパッケージです。このツールは glTFast のアドオンとして動作して、テクスチャのインポート中にその設定を書き換えることができます。これで画像サイズを縮小したり、テクスチャ圧縮を有効化したりできます。

この他にも解決のアプローチはあると思いますが、ともかく、何らかの調整をここでは行うことをお勧めします。
-->

---
layout: two-cols
---

# 音楽 (BGM)

- 音楽生成モデル Lyria 3
- 音楽として破綻していないものを生成可能
- ただし表現力には若干の制約あり
- ゲーム開始時のジングルに使用

::right::

<div class="h-full flex items-center justify-center">
  <video controls class="w-full">
    <source src="/dm-lyria3-example.mp4" type="video/mp4" />
  </video>
</div>

<!--
もうひとつ、最近利用が可能になったモデルに Lyria 3 音楽生成モデルがあります。ちゃんとした音楽を生成できるモデルは今まで存在しなかったんですよね。これでようやく BGM などが作れるようになりました。

ただし、Lyria 3 はものすごく高性能なモデルというわけではありません。一応、音楽として破綻はしていないのですが、ちょっと曲の展開に違和感があったり、単調さが目立ってしまうことが多いです。魅力的な名曲を生み出せるというものではない、と考えた方が良いと思います。

プロトタイプとして、とりあえず何か音を入れておきたい、という用途には十分かもしれません。今回はイントロ部分だけを切り取って、ゲーム開始時のジングルとして使用しました。
-->

---
layout: section
---

# Drift Mayhem まとめ

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
この Drift Mayhem プロジェクトでは、過去のプロジェクトよりも進化した新しいモデル群を使用することができました。主なところでは、Unity Default モデル、Tripo P1 モデル、Lyria 3 モデル、などですね。これらの導入によって Unity AI の実用性は、また更に増強されたと感じました。

Human-in-the-loop 形の開発においては Unity Default は十分な性能を提供してくれましたし、Tripo P1 は 3D モデル生成において初めて満足のいくクオリティの出力を行ってくれました。これらのモデルを活用することにより、3D でアセットを活用したゲームでも、非常に効率良くプロトタイピングを行うことができるようになったと思います。
-->

---
layout: image-right
image: /dm-dirty-code.png
---

# コードの劣化

- 実装作業優先で整理整頓は後回しにした。
- リファクタリングは全く行わなかった。
- その結果、コードはかなり劣化した。
  - 古い仕様の残骸が多数存在する。
  - 名前と機能が一致しない。
  - etc...

<!--
その反面、今回は短期間でリファクタリングを行うことなくコーディング作業を重ねていったので、コードの劣化が無視できないレベルになってしまったと感じています。一応、動くコードにはなっているのですが、実態としてはとても汚い状態になっています。クラスやメソッドの機能が名前と一致していなかったり、重複する機能の実装が複数存在していたり、使用していない機能や古い仕様の残骸が残っていたり、等々です。

例えば、このプロジェクトでは敵のオブジェクトを表す言葉として "Target", "Dummy", "Enemy", "Drone" という単語が混在しています。それぞれが何を意味するのか整理しないまま、追加を重ねていったので、実態が分かりにくくなっています。コードとしては非常に危険な状態ですね。

これらの劣化したコードは、ここから更に開発を続けるならば、整理を行う必要があります。というのも、コーディングエージェントも結局は人間と同じように、クラス名やメソッド名、コメントやドキュメント等々のテキスト情報を手掛かりに開発を進めていくので、そこに混乱があれば、AI もまた混乱してしまいます。結局は、人間の読みやすいコードが AI にとっても理想である、ということですね。
-->

---
layout: image-right
image: /dm-dirty-code2.png
---

# Unity 開発プラクティスの欠落

- Unity 開発のプラクティスを踏襲していない。
  - オブジェクトプール未使用
  - Rigid Body を多数使用したエフェクト

<!--
また、Unity の使い方としても、一般的な開発プラクティスを疎かにした状態になっています。例えば、弾丸はオブジェクトプールを使用せずに毎回使い捨てになっていますし、破壊エフェクトは Particle System を使わずに、わざわざ複数の Rigid Body を生成しています。これらも、ここから先へ開発を進めていこうとするならば、改善しておかなければいけないポイントでしょう。
-->

---

# リファクタリングの重要性

- 指示すればちゃんと改善できる。
- 立ち止まる余地なく要素追加を続ければ劣化する。
- 本格的な開発を続けるならば意識的なリファクタリングが必要。

<!--
もちろん AI コーディングエージェントは、これらの改善方法を正しく把握しています。改善して下さいと指示すれば、問題なく改善作業を行ってくれます。ただ、そう伝えない限りは、ゲーム自体の実装作業の方を優先する、という感じですね。なので、あれを作って下さい、これを作って下さい、と次々に指示すれば、そういった作業の方を優先して、立ち止まることは無くなってしまうようです。

Unity を使用してきたユーザーの方々だったら、こういった危険なシグナルは察知することができると思うのですが、例えば Unity AI を使って初めて Unity を触る、というような方々には、ここは落とし穴になる可能性があるかもしれないと感じました。そういった場合には、エージェントに対して設計のチェックやリファクタリングを行うよう、意識的に対策を講じていく必要があるかもしれません。
-->

---
layout: cover
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

<SlidevVideo muted autoplay loop class="flex-1 min-h-0 w-full object-contain mt-4">
  <source src="/ms-demo-hq.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
今までのプロジェクトはゲームをテーマとしてきましたが、最後のこれだけは純粋に技術的なデモです。3D メッシュオブジェクトを任意の平面で切断すると言う機能を実装しました。また、そのインタラクティブ・デモとして、マウス操作で物理オブジェクトを切り刻める、と言うものを作ってみました。
-->

---

# 開発背景

- MCP Server と外部エージェントを使った長時間実行タスクのテスト

<!--
開発背景についてですが、このプロジェクトは MCP Server を利用した長時間タスクの実行を試すために立ち上げたものです。フロンティアモデルを使用した AI 駆動開発においては、数十分とか数時間、数十時間といった長時間にわたるセッションを人間の手の介在無しに自律実行するわけですが、Unity の AI Assistant は、現状そのような用途に特化されていません。もしそのような開発スタイルを実践したいと思ったら、外部の AI エージェントから MCP を使って Unity Editor と連携する必要があります。
-->

---

# テスト可能性

- 長時間タスクは自動テスト対応が必須
- ゲーム開発は人間の主観に頼る部分が多い
- いかに自動テスト可能な要素を分離するか

<!--
そして、このような長時間タスクの自律実行において必須となるのが testability です。そこで取り組むタスクは自動テストによって検証が可能でなければならない、ということですね。そうでなければ、人間のチェックが必要になってしまい、そこでタスクは止まってしまいます。

ここで問題となるのは、ゲーム開発における課題の多くが、人間の主観的なチェックを必要とするということです。ここまでに作ってきたゲームプロジェクトも、そのほとんどのタスクは、人間の評価を必要とするものでした。

ゲーム開発においても、実際には自動テスト可能なタスクは沢山存在します。ただ、今回ここで扱っているような規模のカジュアルゲームでは、なかなか存在しないと言うのが正直なところだと思います。

ただ今後は、こういったテスト可能性が AI 利用の鍵にもなるので、意識的に自動テスト可能な要素というのを独立させ、分離させていくような努力が必要になると思います。
-->

---

# プロジェクトの構成要素

- MeshSlicer クラス
  - Mesh を任意の平面で切断する機能を提供
  - 自動テストを用意
  - Unity MCP Server + Claude Code (Opus 4.8) を使用
- SlicingDemo シーン
  - インタラクティブデモ
  - Unity AI Assistant (Unity Lite) を使用

<!--
以上を前提に、このプロジェクトの構成要素を解説したいと思います。まずは MeshSlicer クラスが存在しています。これが Mesh の切断機能を実装したものになっており、Test Runner を使用した自動テストが用意されていて、動作検証まで自律的に行えるようになっています。そしてこの部分は MCP Server と Opus 4.8 を使用して、長時間タスクとして自律開発を行わせました。

その後に、この機能を使ったインタラクティブデモとして SlicingDemo というシーンと、一連のスクリプト、マウス操作とかを受け取る部分ですね、それを AI Assistant で作成しました。これはそんなに難しくない内容なので Unity Lite を使用しています。
-->

---

# タスク設計

<blockquote>

Unityにおいてメッシュオブジェクトを自由な平面で切断する機能を実装してください。

この機能は、MeshとUnity.Mathematics.Geometry.Planeで表現される平面を与えると、そのMeshを切断してできる２つのMeshを生成して返します。それぞれの切断面には蓋が追加されます。

ソースとなるMeshは、いわゆる2-manifold/watertight条件が満たされている前提とします。 

頂点データは、position, normal, tangent, uv0まで対応します。切断面のuv0は(0,0)に固定とします。

...
</blockquote>

---

# タスク設計（続き）

<blockquote>
...

ここではTDD的なアプローチを用いるものとします。すなわち、機能の実装を行う前に網羅的なテストを実装する必要があります。テストの実行にはUnity標準のTest Runnerを使用します。

テストには凸メッシュだけでなく、断面が複数ループ・入れ子（穴あき／アニュラス）になるケースを含めます。具体的にはトーラス、中空パイプ、開いた箱（トレイ状）、ボウル形状を含め、各断面で蓋が正しく閉じることを検証します。また、プロジェクトに含まれているfbxモデルも使用します。

実装は最初に最適化を考えない形で行います。ここでは正しさを重視し、パフォーマンスは考慮しません。その実装が完成したら、Mesh Rendererを使ってシーン上でのレンダリングも行い、あなた（AIエージェント）の視覚を利用した定性的な検証も行います。

次にパフォーマンスを計測します。ここでは、メソッド単体でのパフォーマンスと、システム総合でのパフォーマンスと、両方を分けて計測します。後者については、適量のハイポリメッシュを毎フレーム切断したうえでMesh Rendererで描画することで、描画まで含めた負荷を測るものとします。

それらが完了したのちに最適化を開始します。ここではBurstコンパイラ、C# Job Systemを使用しつつ、NativeArrayやAdvanced Mesh APIを活用することでなるべく配列コピーを防ぐような工夫を盛り込みます。ここでは前述のパフォーマンス計測方法を使用してその効果を確認します。繰り返し何度か最適化を試み、妥当な成果が得られたところで作業完了とします。

</blockquote>

<!--
これが実際に使用したプロンプトですね。ざっくりと大まかに要件を述べつつ、Test Driven Development 的な手法で進めるように指示しています。また、ナイーブな実装で基本的な動作を確定させてから、それをベースに最適化を行うように指示しています。つまり、計画、実装、確認、改良、というようなループを自律的に回すよう指示しているわけですね。
-->

---

<div class="h-full flex flex-col">

# 長時間タスクの実行

<SlidevVideo muted autoplay controls class="flex-1 min-h-0 w-full object-contain">
  <source src="/ms-long-session.mp4" type="video/mp4" />
</SlidevVideo>

</div>

<!--
これは実際に実行している様子を早回しにしたものですね。完了までに約40分費やしています。今どきの長時間タスクでは何時間も自律的に実行するケースが少なくないので、これはまあ可愛いものですが、それでも AI Assistant でこのようなタスクを実行するのは難しいので、MCP Server と外部エージェントの組み合わせならではの光景ではあります。
-->

---

# 長時間タスクの実行（続き）

- 実装完了
- パフォーマンス比較

**Performance (20,480-triangle icosphere, Editor)**

| Naive | Burst | Speedup |
|---|---|---|
| 9.16 ms | 1.04 ms | 8.8x |

<!--
そして約40分後にタスクが完了しました。最適化の結果、パフォーマンスはX倍程度になったと報告されていますね。

あとのインタラクティブデモ部分については、これまでのプロジェクトと大差無いので割愛します。
-->

---
layout: two-cols-video
---

# 手動テスト

- 特定のアングルで穴が生じる不具合

::right::

<SlidevVideo muted autoplay loop>
  <source src="/ms-corner-cases.mp4" type="video/mp4" />
</SlidevVideo>

<!--
それで、これで完成しました、となればハッピーエンドなのですが、実際にはそう上手くはいきませんでした。一見うまく動いているのですが、たまに切断面に穴が生じるという不具合が発生しました。

これをテストするために切断面を手動で微調整できるテスト用シーンを作ってもらい、不具合の生じる条件を手動で特定しました。そして、その条件を保存したうえで、AI エージェントに原因を特定してもらう、というワークフローを経ました。

結果として、切断面がメッシュのエッジをかすめるように交差する場合に、このような現象が発生することがある、ということが分かりました。この問題をちゃんと解決することはかなり難しいのですが、今回のようなゲーム用途の場合は、切断面を少しだけズラすということが許されます。そこで、問題が発生する状況を検出したら、切断面を少しだけズラして問題を回避する、というコードを組み込んでもらうことにしました。その結果として、動画でお見せしたような非常に安定した挙動が得られるようになりました。
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
その他に、このプロジェクトでは MCP Tools の機能も使用しました。これは AI Assistant に外部の MCP クライアントを登録して使えるようにするというものですね。MCP Server の機能と混同しないように気をつけて下さい。Unity MCP Server は外部の AI エージェントが Unity を操作可能にするもので、これは Unity AI Assistant から外部のツールを操作する、というものです。

ここでは 3D モデルを、いわゆるマニフォールドモデルとかソリッドモデルとか言われる「切断可能なモデル」に変換するための加工を Blender に行ってもらうことにしました。

3D モデルをマニフォールドモデルに変換するには、Blender の機能をいくつか組み合わせて使用する必要があるのですが、この AI Assistant が自動的に行えるようにした訳ですね。
-->

---

<div class="h-full flex flex-col">

# MCP Tools 設定

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
また、その Blender の機能を呼び出す部分については、AI Assistant のスキル機能を活用することにしました。スキルというのは、AI エージェントによくある機能ですが、ツールの使い方や定型的な手続きを教えるための仕組みですね。これによって、Blender の機能をどういう風に呼び出せばスライス可能なモデルを作れるか、というのを教え込む事ができる訳です。

プロジェクト毎のスキルは "Assets/Skills" ディレクトリの中に配置します。

スキル関係の設定は Preference の中にあります。ここに配置したプロジェクトスキルがリストアップされるはずです。デフォルトでは "Deny" になっていると思うので、"Allow" に変更して下さい。

このような MCP Tools とスキルの組み合わせによって、マニフォールドモデル変換が完全に自動化されました。AI Assistant に「このモデルをマニフォールド化して」と命令すれば、あとは勝手に Blender を呼び出して変換してくれるようになったわけですね。

このように、AI Assistant の MCP Client 機能とスキル機能は、外部アプリやサービスとの連携を自動化するにあたって便利な機能ですので、そのような要素がある場合にはぜひ試してみて下さい。
-->

---

# まとめ

- MCP Server は外部エージェントを使用した長時間タスクの実行に便利
- MCP Client 及びスキル機能は外部ツールとの連携に便利

<!--
まとめです。このように、MCP Server を使用することによって、外部エージェントを使った長時間タスクの実行が可能になります。最近は Unity AI でもフロンティアレベルのモデルが利用可能になってきているので、必ずしも外部のエージェントを使わなくてはならないという訳ではないですが、長時間タスクの実行や開発ループの構築に関しては、やはりメジャーなエージェントにノウハウが蓄積されていますので、そちらを使うメリットが大きいのかなと思いました。

また、MCP Client 機能については、Unity AI Assistant から外部ツールを操作するのに使えることが分かりましたし、その手続きを整理するのにカスタムスキル機能が有効なことも分かりました。
-->
