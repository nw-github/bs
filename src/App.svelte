<script lang="ts">
  import Image from "./lib/Image.svelte";
  import { COUNTERED_BY, COUNTERS } from "./lib/counters";

  const modes = ["Countered By", "Counters"] as const;
  type Mode = (typeof modes)[number];

  const dict = {
    "Countered By": COUNTERED_BY,
    Counters: COUNTERS,
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

  <div class="data">
    {#each dict[currentMode] as [brawler, counters]}
      {#if counters.length && brawler.toLowerCase().includes(query.toLowerCase())}
        <div><Image {brawler} /></div>
        <div class="counters">
          {#each counters as counter}
            <Image brawler={counter} />
          {/each}
        </div>
      {/if}
    {/each}
  </div>
</main>

<style>
  .header {
    padding-bottom: 2em;
  }

  .data {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 2.5fr;
  }

  .counters {
    display: flex;
    overflow: scroll;
    width: 100%;
    align-items: center;
    padding-left: 2em;
  }

  .searchbox {
    border-radius: 0.5em;
    padding: 0.5em 0.5em;
    min-width: 30%;
    max-width: 44%;
  }

  select {
    border-radius: 0.5em;
    padding: 0.5em 0.5em;
  }
</style>
