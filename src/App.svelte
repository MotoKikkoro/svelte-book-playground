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
</script>


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
  <div slot="body">
    <p>SvelteはこれまでにないUIフレームワークです</p>
  </div>
</Card>
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
</style>
