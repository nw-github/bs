<script lang="ts">
  import Image from "./lib/Image.svelte";
  import { COUNTERS } from "./lib/counters";
</script>

<main>
  <table>
    {#each COUNTERS as [brawler, counters]}
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
    text-align: center;
  }

  .bottom-left {
    position: absolute;
    bottom: 8px;
    left: 16px;
  }
</style>
