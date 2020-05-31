# たべるんごのうた

![GitHub Pages](https://github.com/ssssota/taberungo-no-uta/workflows/GitHub%20Pages/badge.svg)

![たべるんごのうたのスクリーンショット](video_ss.png)

ニコニコ動画で一世を風靡した「[たべるんごのうた](https://nico.ms/sm36210300)」。

これを（主に）CSSアニメーションで実装した。
`CSS Houdini`を使っているため、Chrome、もしくはそれに準ずるブラウザじゃないと動かない可能性が高い。

## 仕様

- 若干動きが違う
  - 再現難しい
  - 再現疲れた
  - 画面サイズに依存しないよう％多用した
- テンポが違う
  - CSSなのでms単位で指定できるが算出するのがしんどかった
  - 元動画を0.9倍速くらいでだいたい同じ
- Svelteで実装してある
  - `TaberungoNoUta.svelte`をコピーしたら他で使えるかも
    - SCSSを使っているので要対応
  - 実はブルーバックにする機能がある
    - けど今回は使ってない
    - ブルーバックに限らず、CSSの色なら何でも指定できる
      - もちろんグリーンバックも

## おまけ

[りんごろう.svg](https://github.com/ssssota/ringorou.svg)を作った。
このリポジトリでは使ってない。