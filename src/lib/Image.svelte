<script lang="ts">
  import { IMAGES } from "./counters";

  export let brawler: string;
</script>

{#if IMAGES[brawler]}
  <img src={IMAGES[brawler]} alt={brawler} />
{:else}
  <h1>{brawler}</h1>
{/if}

<style>
  h1,
  img {
    width: 200px;
    height: 200px;
    padding: 2px 5px;
  }

  h1 {
    text-align: center;
    display: inline;
    width: auto;
    height: auto;
  }
</style>
