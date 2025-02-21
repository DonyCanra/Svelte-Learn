<script>
  import svelteLogo from './assets/svelte.svg'
  import Counter from './lib/Counter.svelte'
  import Autocomplete from './lib/Autocomplete.svelte'

  let activeTab = {
      value: '1',
      title: 'Counter',
      desc: 'Menampilkan project counter',
    };
  const tab = [
    {
      value: '1',
      title: 'Counter',
      desc: 'Menampilkan project counter',
    },
    {
      value: '2',
      title: 'Autocomplete',
      desc: 'Menampilkan project search data',
    }
  ]
</script>

<main>
  <div>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>{activeTab.title}</h1>
  <h6>{activeTab.desc}</h6>

  <div class="tabs">
    {#each tab as el}
      <button on:click={() => activeTab = el} class:active={activeTab.value === el.value}>{el.title}</button>
    {/each}
  </div>

  <div class="card">
    {#if activeTab.value === '1'}
      <Counter />
    {/if}
    {#if activeTab.value === '2'}
      <Autocomplete />
    {/if}
  </div>
</main>

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
  .tabs {
    margin-bottom: 1em;
  }
  .tabs button {
    padding: 0.5em 1em;
    margin-right: 0.5em;
    cursor: pointer;
  }
  .tabs button.active {
    background-color: #ff3e00;
    color: white;
  }
  .card {
    margin-top: 1em;
  }
</style>
