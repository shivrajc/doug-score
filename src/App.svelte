<script>
  // import svelteLogo from './assets/svelte.svg'
  // import viteLogo from '/vite.svg'
  // import Counter from './lib/Counter.svelte'
  import AppDesktop from "./AppDesktop.svelte";
  import MediaQuery from './MediaQuery.svelte';
  import AppMobile from "./AppMobile.svelte";
</script>

<main>
  
  <MediaQuery query="(min-width: 800px)" let:matches>
    {#if matches}
      <AppDesktop />      
    {/if}
  </MediaQuery>
  
  <!-- <MediaQuery query="(min-width: 480px) and (max-width: 1200px)" let:matches>
    {#if matches}
      <MobileApp />
    {/if}
  </MediaQuery> -->
  
  <MediaQuery query="(max-width: 800px)" let:matches>
    {#if matches}
      <div class="app-mobile">
        <AppMobile />
      </div>
    {/if}
  </MediaQuery>   
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 1600px;
    /* height: 100vh; */
    text-align: center;
    margin: 0 auto;
  }

  .app-mobile {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
