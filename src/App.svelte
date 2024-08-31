<!-- 親 -->
<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
  import SvelteLogo from './SvelteLogo.svelte';
  import Button from './Button.svelte';
  let buttonLabel='送信';
  let props = {label: '送信', disabled: true};
  import UserProfile from './UserProfile.svelte';
  let taro = { name: '太郎', id: 'taro', bio: 'よろしく'}
  import PropsTest from './PropsTest.svelte';
  import Box from './Box.svelte';
  import Card from './Card.svelte';
  import List from './List.svelte';
  import Count from './Count.svelte';
  import HelloButton from './HelloButton.svelte';

  import {onMount} from 'svelte';
  onMount(()=>{
    const canvas = document.getElementById('canvas');//キャンバス要素を取得
    const ctx = canvas.getContext('2d');//2D描画コンテキストを取得
    ctx.fillStyle= '#ddd'; // 塗りつぶしの色
    ctx.fillRect(0,0,100,100);
    ctx.fillRect(100,100,200,200);
    // fillRect は、描画エリア内での矩形の位置とサイズを決定
  });

  import {onDestroy} from 'svelte';
  let now = new Date(); //現在の日時を取得して now という変数に保存しています。この変数はリアクティブで、時間が経過するとともに更新される
  const timer = setInterval(()=>{
    now = new Date();
  }, 1000); // setInterval を使って、1秒（1000ミリ秒）ごとに now 変数を更新するタイマーを設定
  // setInterval は、指定された時間間隔で関数を繰り返し実行するJavaScriptのタイマー関数
  onDestroy(()=>{
    clearInterval(timer);
  }); // clearInterval(timer); を実行して、タイマーを停止


  // 投稿0~99までの配列を作成
  let contents = Array.from({length: 100}, (_, i)=> `投稿${i}`);
  import {beforeUpdate, afterUpdate} from 'svelte';
  let prevHeight;
  beforeUpdate(()=>{
    const element = document.getElementById('timeline');
    if (element){
      //DOM更新直前の要素のscrollHeightを保存
      prevHeight = element.scrollHeight;
    }
  });
  afterUpdate(()=>{
    if(prevHeight){
      //更新後にscrollHeightが増えた分だけスクロール位置を調整
      const element = document.getElementById('timeline');
      const diff = element.scrollHeight - prevHeight;
      element.scrollTop += diff;
    }
  });

  function handleClick(){
    // タイムラインの先頭に項目を追加
    contents = [
      ...Array.from({length: 100}, (_, i) => `投稿${i-100}`),
      ...contents,
    ];
  }


  function handleSubmit(event) {
    const formData = new FormData(event.target);
    alert(`検索キーワードは${formData.get('q')}です。`)
  }

  function handleDivClick(){
    alert('divをクリックしました');
  }

  function handleButtonClick(){
    alert('buttonをクリックしました');
  }

  function handleHello(event){
    alert(event.detail);
  }



</script>

<canvas id="canvas" width=200 height="200"></canvas>
<!-- <canvas> の width と height は、キャンバスの全体的な描画エリアを定義\ -->


<main>
  <div>
    <a href="https://vitejs.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <div class="card">
    <Counter />
  </div>

  <div id="timeline">
    {#each contents as item}
      <div>{item}</div>
      {/each}
  </div>

  <p>
    Check out <a href="https://github.com/sveltejs/kit#readme" target="_blank" rel="noreferrer">SvelteKit</a>, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p>
</main>

<PropsTest foo="テスト" bar={42}> </PropsTest>

<!-- Boxにコンテンツがある場合 -->
<Box>
  <h3> Svelteについて</h3>
  <p>SvelteはこれまでにないUIフレームワークです </p>
  <Button {...props}></Button> 
</Box>

<!-- Boxにコンテンツがない場合 ⇒Box.svelteの<em>に記載した内容が表示-->
<Box>
</Box>

<div>Svelteのロゴ画像が差し込まれる</div>
<SvelteLogo></SvelteLogo>
<!-- <Button label={buttonLabel}></Button> -->

<Card>
  <h3 slot="title">Svelteについて</h3>
  <div>
    <p>SvelteはこれまでにないUIフレームワークです</p>
  </div>
</Card>

<List let:item={text}>
  <div class="item">{text}</div>
</List>

<Count>
  <span slot="count" let:value={v}>{v}</span>
</Count>

<button on:click={handleClick}>タイムラインを更新</button>

<form on:submit|preventDefault={handleSubmit}>
  <input type="search" name="q">
  <button type="submit">検索</button>
</form>

<div on:click|capture|stopPropagation={handleDivClick}>
  <button on:click={handleButtonClick}>Divクリック</button>
</div>

<HelloButton on:hello={handleHello} />

<div>現在の時刻は{now.toLocaleString()}です。</div>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
  .item{
    color: blue;
  }
  #timeline{
    width: 300px;
    height: 300px;
    border: 1px solid gray;
    overflow: auto;
  }
</style>
