---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS (experimental)
css: unocss
---

# CSS コンテナクエリーについて

---

# 自己紹介

<h2>橘井 貴輝</h2>

- PDU所属のFE
- 趣味: ハードコア・パンク、ヒップホップ、映画をひたすら見る
- FE勉強会やってます！（火曜の12時~13時）

<div style="display: flex; gap: 100px">
<img src="workroom.jpg" alt="" width="300">
<img src="workroom2.jpg" alt="" width="300">
</div>

---

# Agenda

- コンテナクエリーとは？
- メディアクエリーについて
- メディアクエリーの使いにくい部分
- コンテナクエリーだと
- 使用例
- まとめ

---

# コンテナクエリーとは？

<div style="display: flex; justify-content: center; height: 80%; align-items: center">
<h3>親要素の大きさに応じてスタイルを調整可能な仕様（実験段階）</h3>
</div>

---

# コンテナクエリーとは？

- CSS Containment の一部となる予定の仕様
  - 日本語訳では「CSS 封じ込め」
  - ウェブページの表示性能を向上させるため、ページの任意のサブツリーをそれ以外の部分から独立させるのを目的としている

---

# CSS Containment の基本的な例

各記事が、他の記事と独立していることをブラウザに伝えるために指定をする<br/>
ブラウザ自身は、記事が自己完結しているかどうかは判断できない

<div style="display: flex; gap: 100px">
<div style="width: 400px">
```html
<h1>私のブログ</h1>
<article>
  <h2>良い記事の見出し</h2>
  <p>内容はこちら。</p>
</article>
<article>
  <h2>他の記事の他の見出し</h2>
  <p>さらなる内容はこちら。</p>
</article>
```
</div>

<div style="width: 200px">
```css
article {
  contain: content;
}
```
</div>

</div>

参照: https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Containment#%E5%9F%BA%E6%9C%AC%E7%9A%84%E3%81%AA%E4%BE%8B

---

# メディアクエリーについて

- ウィンドウの幅に応じて、スタイルを調整することができる
  - 「幅が広い場合は横並びにして、狭い場合は1列で表示して」的な
  - PCとスマートフォンそれぞれでスタイルを変えたり
  - `@media` 以降に条件を書いていく

```css
@media (max-width: 1280px) { ... }
```

---

# メディアクエリーの使いにくい部分

画面幅に応じて、カードコンポーネントを表示する数を制御しなければならない（増えてはいないけど）

<MediaQuery />

---

# メディアクエリーの使いにくい部分

例として洗い出すとこんな感じ

- （0 ~ 479px）: カードを2列表示
- （480px ~ 767px）: カードを3列表示
- （768 ~ 1023px）: カードを4列表示
- （1024px ~ 1199px）: カードを3列表示
- （1200px ~ ）: カードを4列表示

---

# メディアクエリーの使いにくい部分

<h4>条件が多くなると、メディアクエリーで表現するのが大変になる！
🤯🤯🤯🤯🤯🤯🤯🤯🤯🤯🤯🤯</h4>

```css
@media (min-width:480px) {
  .card {
    width: 3列表示にしたい;
  }
  /* 何らかのスタイル  */
}

@media (min-width: 768px) {
  .card {
    width: 4列表示にしたい;
  }
  /* 何らかのスタイル  */
}

@media (min-width: 1024px) {
  .card {
    width: ３列表示にしたい;
  }
  /* 何らかのスタイル  */
}

@media (min-width: 1200px) {
  .card {
    width: 4列表示にしたい;
  }
}
```

---

# コンテナクエリーだと

直接の親要素の幅によって見た目を調節できる

<img src="container_example.png" alt="" style="height: 350px" />

出典: https://ishadeed.com/article/say-hello-to-css-container-queries/

---

# コンテナクエリーだと

メインカラムの幅だけを考えてスタイルを書くことができる

<MediaQuery2 />

---

# コンテナクエリーだと

画面の幅や、サイドバーがどこにあるかなどが関係なくなる

```css
@container(min-width:480px) {
  .item {
    width: 3列表示にしたい;
  }
}
@container(min-width:768px) {
  .item {
    width: 4列表示にしたい;
  }
}
```

---

# コンテナクエリーの使い方

- Chromeのアドレスバーに `chrome://flags` と入力して、 `container queries` を有効にする
- まずは、 `contain` プロパティを追加する
  - これによってページ全体ではなく、影響を受けるエリアを指定して、再描画するようにブラウザに伝えることができる

```css
.item {
  contain: layout inline-size;
}
```

---

# コンテナクエリーの使い方

- 次に、コンテナクエリを機能させるスタイルを追加する
  - `@container` アットルールを利用する

```css
.item {
  contain: layout inline-size;
}

@container (min-width: 400px) {
  .article {
    display: flex;
    flex-wrap: wrap;
  }
  
  /* 他のスタイルを記述していく */
}

```

---

# コンテナクエリーの使用例

ページネーション<br />
幅が狭ければボタンのみ、広ければページ数も表示など

<div style="display: flex; justify-content: space-between">
<img src="pagination.png" alt="" style="width: 480px; height: 300px" />

<div style="height: 320px; width: 300px; overflow: scroll">
```css
.wrapper {
  contain: layout inline-size;
}

@container (min-width: 250px) {
  .pagination {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .pagination li:not(:last-child) {
    margin-bottom: 0;
  }
}

@container (min-width: 500px) {
  .pagination {
    justify-content: center;
  }

  .pagination__item:not(.btn) {
    display: block;
  }

  .pagination__item.btn {
    display: none;
  }
}
```
</div>
</div>



---

# コンテナクエリーの使用例

プロフィールのカード

<div style="display: flex; justify-content: space-between">
<img src="profile.png" alt="" style="width: 540px; height: 200px" />

<div style="height: 320px; width: 300px; overflow: scroll">
```css
.p-card-wrapper {
  contain: layout inline-size;
}

.p-card {
  /* デフォルトのスタイルを記述 */
}

@container (min-width: 450px) {
  .meta {
    display: flex;
    justify-content: center;
    gap: 2rem;
    border-top: 1px solid #e8e8e8;
    background-color: #f9f9f9;
    padding: 1.5rem 1rem;
    margin: 1rem -1rem -1rem;
  }

  /* 他のスタイルがあればここに記述 */
}
```
</div>
</div>


---

# まとめ

- 画面全体ではなく、細かい粒度でスタイルを管理できるから良さそう
- 実際の仕様化が待たれる