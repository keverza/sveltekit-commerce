<script>
  import ThreeItemGrid from '$components/ThreeItemGrid.svelte';
  import Carousel from '$components/Carousel.svelte';

  /** @type {import('./$types').PageData} */
  export let data;

  $: clothesCollection = data[0]?.node?.products?.edges;
  $: featuredCollection = data[1]?.node?.products?.edges;
</script>

<svelte:head>
  <title>Home – SvelteKit Commerce</title>
</svelte:head>

<main>
  <section>
    <div class="">
      <ThreeItemGrid products={featuredCollection} />
    </div>
  </section>
  <section>
    <Carousel items={clothesCollection} />
  </section>
  <section>
    <div class="">
      <div class="">Dessert dragée halvah croissant.</div>
      <div>
        <div class="">
          Cupcake ipsum dolor sit amet lemon drops pastry cotton candy. Sweet carrot cake macaroon
          bonbon croissant fruitcake jujubes macaroon oat cake. Soufflé bonbon caramels jelly beans.
          Tiramisu sweet roll cheesecake pie carrot cake.
        </div>
        <button class=""> Read it here </button>
      </div>
    </div>
  </section>
</main>
