<script lang="ts">
  import Image from "./lib/Image.svelte";
  import { COUNTERS } from "./lib/counters";

  let query = "";
</script>

<main>
  <input class="searchbox" type="text" placeholder="Search..." bind:value={query} />

  <table>
    {#each COUNTERS as [brawler, counters]}
      {#if brawler.toLowerCase().includes(query.toLowerCase())}
        <tr>
          <td class="container">
            <Image {brawler} />
            <div class="bottom-left">{brawler}</div>
          </td>
          <td class="counters">
            {#each counters as counter}
              <Image brawler={counter} />
            {/each}
          </td>
        </tr>
      {/if}
    {/each}
  </table>
</main>

<style>
  .counters {
    display: flex;
    padding-left: 100px;
  }

  .container {
    position: relative;
  }

  .bottom-left {
    position: absolute;
    bottom: 8px;
    left: 16px;
    opacity: 0;
  }

  .searchbox {
    border-radius: 5px;
    padding: 5px 5px;
    width: 300px;
  }
</style>
