<script>
  import { Canvas } from '@threlte/core';
  import Scroller from "@sveltejs/svelte-scroller";
  import Scene from '$lib/Scene.svelte';
  import ScrollerData from '$lib/ScrollerData.svelte';

  let index, offset, progress;

  const sections = Array(10).fill('x');

</script>

<Scroller bind:index bind:offset bind:progress>
<div slot="background" class="canvas-wrapper">
  <Canvas>
    <Scene {index} {offset} {progress}/>
  </Canvas>
</div>
<div slot="foreground" class="content">
  <div class="scroller-data">
    <ScrollerData {index} {offset} {progress} />
  </div>

  <header>
    <div class="intro">
      <h1>Threlte x Scroller</h1>
      <p>Starter project for scrollytelling scenes with <code>svelte-scroller</code> and <code>threlte</code></p>
    </div>
  </header>

  {#each sections as section, idx}
    <section class:active={index === idx}>
      <h1>Section {idx}</h1>
    </section>
  {/each}  
</div>
</Scroller>


<style>
  .canvas-wrapper {
    position: absolute;
    width: 100%;
    height: 100vh;
    background: #161616;
    overflow: hidden;
  }

  .content {
    padding: 0 0 25vh;
  }

  header {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  header .intro {
    width: 90%;
    max-width: 400px;
    padding: 1rem;
    margin: 0 auto;
    color: #fafbfc;
    background-color: #00000088;
  }

  section {
    height: 500px;
    max-width: 100%;
    width: 500px;
    margin: 10rem auto;
    border: 2px solid white;
    color: #ffffff;
  }

  section.active {
    border: 2px solid #00ff00;
  }

  .scroller-data {
    position: fixed;
    top: 0;
    width: 100%;
    z-index: 1;
  }

</style>