<script lang="ts">
  import Image from "./lib/Image.svelte";
  import { COUNTERED_BY, COUNTERS } from "./lib/counters";

  const modes = ["Countered By", "Counters"] as const;
  type Mode = (typeof modes)[number];

  const dict = {
    "Countered By": COUNTERED_BY,
    "Counters": COUNTERS,
  };

  let query = "";
  let currentMode: Mode = "Countered By";
</script>

<main>
  <div class="header">
    <input class="searchbox" type="text" placeholder="Search..." bind:value={query} />
    <select name="mode" id="mode" bind:value={currentMode}>
      {#each modes as mode}
        <option value={mode}>{mode}</option>
      {/each}
    </select>
  </div>

  <table>
    {#each dict[currentMode] as [brawler, counters]}
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
