<script>
  import { afterUpdate, onMount } from 'svelte';
  export let background = '#fff';
  export const play = () => active = true;
  export const stop = () => active = false;
  let displayElement;
  let active = false;
  let isLoading = true;

  const resize = () => {
    const displayRect = displayElement.getBoundingClientRect();
    document.querySelectorAll('.lyric').forEach(lyricElem => {
      lyricElem.style.fontSize = `${displayRect.width / 18}px`;
    });
  }

  onMount(resize);
  afterUpdate(resize);
  addEventListener('resize', resize);

  if (window.CSS && CSS.registerProperty) {
    CSS.registerProperty({ name: '--akaringo-scale-x', syntax: '<number>', inherits: false, initialValue: '1' });
    CSS.registerProperty({ name: '--akaringo-scale-y', syntax: '<number>', inherits: false, initialValue: '1' });
    CSS.registerProperty({ name: '--akaringo-translate-x', syntax: '<length-percentage>', inherits: false, initialValue: '0' });
    CSS.registerProperty({ name: '--akaringo-translate-y', syntax: '<length-percentage>', inherits: false, initialValue: '0' });
    CSS.registerProperty({ name: '--akaringo-rotate', syntax: '<angle>', inherits: false, initialValue: '0deg' });
    CSS.registerProperty({ name: '--akaringo-rotate-y', syntax: '<angle>', inherits: false, initialValue: '180deg' });
    CSS.registerProperty({ name: '--ringorou-scale-x', syntax: '<number>', inherits: false, initialValue: '1' });
    CSS.registerProperty({ name: '--ringorou-scale-y', syntax: '<number>', inherits: false, initialValue: '1' });
    CSS.registerProperty({ name: '--ringorou-rotate', syntax: '<angle>', inherits: false, initialValue: '0deg' });
    CSS.registerProperty({ name: '--ringorou-translate-x', syntax: '<length-percentage>', inherits: false, initialValue: '0' });
    CSS.registerProperty({ name: '--ringorou-translate-y', syntax: '<length-percentage>', inherits: false, initialValue: '0' });
  }
</script>

<div
  bind:this={displayElement}
  class="taberungo-no-uta"
  class:active
  style="background-color:{background};"
>
  {#if isLoading && !active}
    <div class="loading">
      <div class="loader">
        <p>フォント読み込み</p>
        <div class="loader-akaringo-1"></div>
        <div class="loader-akaringo-2"></div>
        <div class="loader-akaringo-3"></div>
        <div class="loader-akaringo-4"></div>
        <div class="loader-ringorou"><img src="./images/りんごろう.png" alt="りんごろうの画像"></div>
      </div>
      <div class="loading-status">
      </div>
      <div class="loading-icon">
        <p class="loading-text">Tap to start!</p>
      </div>
    </div>
  {:else if active}
    <div class="ringorou images">
      <img src="./images/りんごろう.png" alt="りんごろうの画像" class="image">
    </div>
    <div class="akaringo images">
      <div class="image"></div>
    </div>
    <div class="lyrics">
      <p class="lyric">たーべるんごー　たべるんごー</p>
      <p class="lyric">やまがたりんごを　たべるんごー</p>
      <p class="lyric">おいしいりんごを　たべるんごー</p>
      <p class="lyric">いっぱいたべるんごー（ﾝｺﾞｰ）</p>
      <p class="lyric">たーべるんごー　たべるんごー</p>
      <p class="lyric">やまがたりんごを　たべるんごー</p>
      <p class="lyric">あーまいりんごを　たべるんごー</p>
      <p class="lyric">もりもりたべるんごー（ﾝｺﾞｰ）</p>
      <p class="lyric">こいつはりんごろう（ﾝｺﾞｰ）</p>
    </div>
  {/if}
</div>

<style type="text/scss">
@font-face {
  font-family: 'Senobi-Gothic';
  src:
    url('../fonts/Senobi-Gothic-Bold.woff2') format('woff2'),
    url('../fonts/Senobi-Gothic-Bold.woff') format('woff'),
    url('../fonts/Senobi-Gothic-Bold.ttf') format('truetype');
}

.taberungo-no-uta {
  font-family: 'Senobi-Gothic', sans-serif;
  background: white;

  .loading {
    width: 100%;
    height: 100%;
    .loader {
      visibility: hidden;
      .loader-akaringo-1 { background: url('../images/あかりんご1.png'); }
      .loader-akaringo-2 { background: url('../images/あかりんご2.png'); }
      .loader-akaringo-3 { background: url('../images/あかりんご3.png'); }
      .loader-akaringo-4 { background: url('../images/あかりんご4.png'); }
    }
    .loading-icon {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 30px;
      height: 30px;

      &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        box-sizing: border-box;
        border: 5px solid rgba(0,0,0,0.5);
        animation: loading-spin 1s ease-in-out 0s infinite normal none;
      }

      .loading-text {
        transform: translateX(-50%);
      }
    }

  }

  &.active {
    .lyrics {
      width: 100%;
      height: 100%;
      color: black;

      .lyric {
        margin: 0;
        padding: 0;
        position: absolute;
        bottom: 0;
        left: 50%;
        width: 100%;
        text-align: center;
        transform: translate(-50%, -10%);
        font-size: 320%;

        &:nth-child(1) { animation: hide 0s linear 2s 1 normal both; }
        &:nth-child(2) { animation: show 0s linear 2s 1 normal backwards, hide 0s linear 4s 1 normal forwards; }
        &:nth-child(3) { animation: show 0s linear 4s 1 normal backwards, hide 0s linear 6s 1 normal forwards; }
        &:nth-child(4) { animation: show 0s linear 6s 1 normal backwards, hide 0s linear 8s 1 normal forwards; }
        &:nth-child(5) { animation: show 0s linear 8s 1 normal backwards, hide 0s linear 10s 1 normal forwards; }
        &:nth-child(6) { animation: show 0s linear 10s 1 normal backwards, hide 0s linear 12s 1 normal forwards; }
        &:nth-child(7) { animation: show 0s linear 12s 1 normal backwards, hide 0s linear 14s 1 normal forwards; }
        &:nth-child(8) { animation: show 0s linear 14s 1 normal backwards, hide 0s linear 16s 1 normal forwards; }
        &:nth-child(9) { animation: show 0s linear 16s 1 normal both; }
      }
    }

    .images {
      position: absolute;
      width: 100%;
      height: 100%;

      .image {
        position: absolute;
      }

      &.akaringo {
        .image {
          top: 15%;
          left: 33%;
          width: 30%;
          height: 68%;
          background-size: contain;
          background-repeat: no-repeat;

          transform-origin: bottom center;
          transform:
            scale(var(--akaringo-scale-x), var(--akaringo-scale-y))
            translate(var(--akaringo-translate-x), var(--akaringo-translate-y))
            rotate(var(--akaringo-rotate))
            rotateY(var(--akaringo-rotate-y));
          animation:
            akaringo-image-1      0s    linear 0s     1 normal  forwards,
            akaringo-move-back    1s    linear 0s     1 normal  forwards,
            akaringo-jump         1.1s  linear 0s     1 normal  none,
            akaringo-image-2      0s    linear 0.5s   1 normal  forwards,
            akaringo-turn-a       1.1s  linear 1.1s   1 normal  none,
            akaringo-jump         1.1s  linear 2.2s   1 normal  none,
            akaringo-image-4      0s    linear 3s     1 normal  forwards,
            akaringo-step         0.7s  linear 3.3s   1 normal  none,
            akaringo-turn-a       1s    linear 4s     1 normal  none,
            akaringo-image-3      0s    linear 4.2s   1 normal  forwards,
            akaringo-move-back    1s    linear 4s     1 reverse forwards,
            akaringo-jump         1s    linear 5s     1 normal  none,
            akaringo-image-1      0s    linear 6s     1 normal  forwards,
            akaringo-lean-a       1s    linear 6s     1 normal  none,
            akaringo-jump         1s    linear 7s     1 normal  none,
            akaringo-flip         0s    linear 8s     1 normal  forwards,
            akaringo-move-forward 1s    linear 8s     1 normal  forwards,
            akaringo-jump         1.1s  linear 8s     1 normal  none,
            akaringo-image-2      0s    linear 8.5s   1 normal  forwards,
            akaringo-turn-b       1.1s  linear 9.1s   1 normal  none,
            akaringo-jump         1.1s  linear 10.2s  1 normal  none,
            akaringo-image-4      0s    linear 11s    1 normal  forwards,
            akaringo-step         0.7s  linear 11.3s  1 normal  none,
            akaringo-turn-b       1s    linear 12s    1 normal  none,
            akaringo-image-3      0s    linear 12.2s  1 normal  forwards,
            akaringo-move-forward 1s    linear 12s    1 reverse forwards,
            akaringo-jump         1s    linear 13s    1 normal  none,
            akaringo-image-1      0s    linear 14s    1 normal  forwards,
            akaringo-lean-b       1s    linear 14s    1 normal  none,
            akaringo-jump         1s    linear 14.7s  1 normal  none,
            akaringo-zoom-out     0.5s  linear 16s    1 normal  forwards,
            akaringo-final-jump   1s    linear 17.2s  1 normal  none;
        }
      }
      &.ringorou {
        .image {
          height: 50%;
          top: 28%;
          left: 65%;

          transform:
            scale(var(--ringorou-scale-x, 0), var(--ringorou-scale-y, 0))
            rotate(var(--ringorou-rotate, 0deg))
            translate(var(--ringorou-translate-x, 0), var(--ringorou-translate-y, 0));
          transform-origin: bottom center;
          animation:
            ringorou-shake 2.55s linear 0s 6 normal none,
            ringorou-jump 0.5s linear 6.5s 1 normal none,
            ringorou-jump 0.5s linear 14.5s 1 normal none,
            ringorou-zoom-in 0.5s linear 16s 1 normal forwards,
            ringorou-final-jump 1s linear 17.2s 1 normal none;
        }
      }
    }
  }
}

/* Loading keyframes */
@keyframes loading-spin {
  0% { transform: translate(-50%, -50%) rotate(0deg); }
  100% { transform: translate(-50%, -50%) rotate(360deg); }
}
/* show/hide keyframes */
@keyframes show {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
@keyframes hide {
  0% { opacity: 1; }
  100% {opacity: 0; }
}
/* Akaringo keyframes */
@keyframes akaringo-flip {
  0% { --akaringo-rotate-y: 180deg; }
  100% { --akaringo-rotate-y: 0deg; }
}
@keyframes akaringo-jump {
  0% { --akaringo-scale-x: 1; --akaringo-scale-y: 1; --akaringo-translate-y: 0; }
  10% { --akaringo-scale-x: 1.05; --akaringo-scale-y: 0.95; --akaringo-translate-y: 0; }
  50% { --akaringo-scale-x: 1; --akaringo-scale-y: 1; --akaringo-translate-y: -3%; }
  80% { --akaringo-scale-x: 1.02; --akaringo-scale-y: 0.98; --akaringo-translate-y: 0; }
  100% { --akaringo-scale-x: 1; --akaringo-scale-y: 1; --akaringo-translate-y: 0; }
}
@keyframes akaringo-final-jump {
  0% { --akaringo-scale-x: 0.9; --akaringo-scale-y: 0.9; --akaringo-translate-y: 0; }
  10% { --akaringo-scale-x: 0.95; --akaringo-scale-y: 0.85; --akaringo-translate-y: 0; }
  50% { --akaringo-scale-x: 0.9; --akaringo-scale-y: 0.9; --akaringo-translate-y: -3%; }
  80% { --akaringo-scale-x: 0.92; --akaringo-scale-y: 0.88; --akaringo-translate-y: 0; }
  100% { --akaringo-scale-x: 0.9; --akaringo-scale-y: 0.9; --akaringo-translate-y: 0; }
}
@keyframes akaringo-move-back {
  0% { --akaringo-translate-x: 0; }
  100% { --akaringo-translate-x: -7.5%; }
}
@keyframes akaringo-move-forward {
  0% { --akaringo-translate-x: 0; }
  100% { --akaringo-translate-x: 7.5%; }
}
@keyframes akaringo-step {
  0% { --akaringo-scale-x: 1; --akaringo-scale-y: 1; }
  50% { --akaringo-scale-x: 1.02; --akaringo-scale-y: 0.98; }
  100% { --akaringo-scale-x: 1; --akaringo-scale-y: 1; }
}
@keyframes akaringo-lean-a {
  0% { --akaringo-rotate: 0deg; }
  50% { --akaringo-rotate: 5deg; }
  100% { --akaringo-rotate: 0deg; }
}
@keyframes akaringo-lean-b {
  0% { --akaringo-rotate: 0deg; }
  50% { --akaringo-rotate: -5deg; }
  100% { --akaringo-rotate: 0deg; }
}
@keyframes akaringo-turn-a {
  0% { --akaringo-rotate-y: 180deg; }
  50% { --akaringo-rotate-y: 0deg; }
  100% { --akaringo-rotate-y: -180deg; }
}
@keyframes akaringo-turn-b {
  0% { --akaringo-rotate-y: 0deg; }
  50% { --akaringo-rotate-y: 180deg; }
  100% { --akaringo-rotate-y: 360deg; }
}
@keyframes akaringo-zoom-out {
  0% { --akaringo-translate-x: 0; --akaringo-translate-y: 0; --akaringo-scale-x: 1; --akaringo-scale-y: 1; }
  100% { --akaringo-translate-x: -55%; --akaringo-translate-y: 0; --akaringo-scale-x: 0.9; --akaringo-scale-y: 0.9; }
}
@keyframes akaringo-image-1 { 100% { background-image: url('../images/あかりんご1.png'); } }
@keyframes akaringo-image-2 { 100% { background-image: url('../images/あかりんご2.png'); } }
@keyframes akaringo-image-3 { 100% { background-image: url('../images/あかりんご3.png'); } }
@keyframes akaringo-image-4 { 100% { background-image: url('../images/あかりんご4.png'); } }
/* Ringorou keyframes */
@keyframes ringorou-shake {
  0% { --ringorou-scale-x: 1; --ringorou-scale-y: 1; --ringorou-rotate: 0deg; }
  25% { --ringorou-scale-x: 1.05; --ringorou-scale-y: 0.95; --ringorou-rotate: 5deg; }
  50% { --ringorou-scale-x: 1; --ringorou-scale-y: 1; --ringorou-rotate: 0deg; }
  75% { --ringorou-scale-x: 1.05; --ringorou-scale-y: 0.95; --ringorou-rotate: -5deg; }
  100% { --ringorou-scale-x: 1; --ringorou-scale-y: 1; --ringorou-rotate: 0deg; }
}
@keyframes ringorou-jump {
  0% { --ringorou-translate-y: 0; }
  50% { --ringorou-translate-y: -5%; }
  100% { --ringorou-translate-y: 0; }
}
@keyframes ringorou-zoom-in {
  0% { --ringorou-translate-x: 0; --ringorou-translate-y: 0; --ringorou-scale-x: 1; --ringorou-scale-y: 1; }
  100% { --ringorou-translate-x: -50%; --ringorou-translate-y: 2%; --ringorou-scale-x: 1.5; --ringorou-scale-y: 1.5; }
}
@keyframes ringorou-final-jump {
  0% { --ringorou-scale-x: 1.5; --ringorou-scale-y: 1.5; --ringorou-translate-y: 2%; }
  10% { --ringorou-scale-x: 1.55; --ringorou-scale-y: 1.45; --ringorou-translate-y: 2%; }
  50% { --ringorou-scale-x: 1.5; --ringorou-scale-y: 1.5; --ringorou-translate-y: -3%; }
  80% { --ringorou-scale-x: 1.52; --ringorou-scale-y: 1.48; --ringorou-translate-y: 2%; }
  100% { --ringorou-scale-x: 1.5; --ringorou-scale-y: 1.5; --ringorou-translate-y: 2%; }
}
</style>
