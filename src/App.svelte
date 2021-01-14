<script lang="ts">
  import { onMount } from "svelte";

  let points = [];
  // $: pointHeaders = points.length > 0 ? Object.keys(points[0]) : [];
  // Read in the json
  onMount(async () => {
    let raw = await fetch("out.json");
    points = await raw.json();
  });
</script>

<main>
  {#each points as point}
    <div>
      <!-- act, components, summary, category, reasoning -->
      <!-- <div>Act</div> -->
      <div class="act">{point.act}</div>

      <!-- <div class="item"> -->
      <!-- </div> -->
      <!-- <div>Components</div> -->
      <!-- <div class="category">{point.category}</div> -->
      <div class="categories">
        {#each point.category.split(", ") as category}
          <span class="category">
            {category}
          </span>
        {/each}
      </div>

      <!-- <div class="components"><i>Entailed the </i>{point.components}</div> -->

      <div class="item">
        <div class="header-summary">Included the</div>
        <div class="summary">{point.components}</div>
      </div>
      <!-- <div>Reasoning</div> -->
      <div class="item">
        <div class="header-summary">Summary</div>
        <div class="summary">{point.summary}</div>
      </div>
      <div class="item">
        <div class="header-reasoning">Reasoning</div>
        <div class="reasoning">{point.reasoning}</div>
      </div>
    </div>
  {/each}
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

  // table {
  //   box-shadow: 0rem 0.1rem 0.3rem 0.1rem lightgray;
  //   border-collapse: collapse;
  //   // border: 1px solid;
  // }

  // th {
  //   font-family: "Bebas Neue", cursive;
  //   font-size: 2rem;
  //   padding: 1rem 1rem 0 1rem;
  //   text-align: left;
  // }

  // td {
  //   // border: 1px solid #2b2b2b20;
  //   border-bottom: 1px solid #2b2b2b20;
  //   padding: 1rem;
  //   text-align: left;
  //   vertical-align: top;
  // }

  // td:nth-child(1) {
  //   vertical-align: middle;
  // }

  // td:nth-child(4) {
  //   vertical-align: middle;
  // }

  .act {
    font-family: "Bebas Neue", cursive;
    font-size: 2rem;
    color: #444444;
  }

  .components {
    // padding-top: -.5rem;
    // padding-bottom: .5rem;
    // padding: 1rem;
    // border-top: 1px dotted gray;
    // border-bottom: 1px dotted gray;
  }

  .category {
    font-size: 0.8rem;
    background-color: lightgray;
    padding: 0.2rem;
    border-radius: 0.2rem;
    font-family: "Courier New", Courier, monospace;
    // margin: 0.5rem;
  }

  .categories {
    // margin: 0.5rem;
    padding: 0 0 0.5rem;
    display: flex;
    flex-direction: row;
    gap: .5rem;
  }

  .header-summary {
    font-style: italic;
    font-size: 0.8rem;
    // padding: 1rem 0rem 1rem;
  }

  .header-reasoning {
    font-style: italic;
    font-size: 0.8rem;
  }

  .item {
    padding: 0rem 0rem 1rem;
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
  @media (min-width: 992px) {
    main {
      width: 50%;
    }
  }

  // Extra large devices (large desktops, 1200px and up)
  @media (min-width: 1200px) {
    main {
      width: 50%;
    }
  }
</style>
