<script lang="ts">
  import { onMount } from "svelte";

  let points = [];
  $: pointHeaders = points.length > 0 ? Object.keys(points[0]) : [];
  // Read in the json
  onMount(async () => {
    let raw = await fetch("out.json");
    points = await raw.json();
  });
</script>

<main>
  <table>
    <tr>
      {#each pointHeaders as header}
        <th>
          {header}
        </th>
      {/each}
    </tr>
    {#each points as point}
      <tr>
        <!-- act, components, summary, category, reasoning -->
        <td class="act">{point.act}</td>
        <td class="components">{point.components}</td>
        <td class="summary">{point.summary}</td>
        <td class="category">{point.category}</td>
        <td class="reasoning">{point.reasoning}</td>
      </tr>
    {/each}
  </table>
</main>

<svelte:head>
  <link rel="preconnect" href="https://fonts.gstatic.com" />
  <link
    href="https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<style lang="scss">
  main {
    // text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  table {
    box-shadow: 0rem 0.1rem 0.3rem 0.1rem lightgray;
    border-collapse: collapse;
    // border: 1px solid;
  }

  th {
    font-family: "Bebas Neue", cursive;
    font-size: 2rem;
    padding: 1rem 1rem 0 1rem;
    text-align: left;
  }

  td {
    // border: 1px solid #2b2b2b20;
    border-bottom: 1px solid #2b2b2b20;
    padding: 1rem;
    text-align: left;
    vertical-align: top;
  }
  
  // td:nth-child(1) {
  //   vertical-align: middle;
  // }
  
  // td:nth-child(4) {
  //   vertical-align: middle;
  // }

  .act {
    // font-family: "Bebas Neue", cursive;
    // font-size: 1.5rem;
    color: #444444;
  }
  
  .category {
    // font-size: 1.5rem;
  }

  // h1 {
  //   color: #ff3e00;
  //   text-transform: uppercase;
  //   font-size: 4em;
  //   font-weight: 100;
  // }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
