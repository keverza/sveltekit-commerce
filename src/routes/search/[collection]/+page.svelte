<script>
  import GridTile from '$components/GridTile.svelte';
  import { page } from '$app/stores';

  /** @type {import('./$types').PageData} */
  export let data;
  let collection;

  $: data.body.collections.forEach((d) => {
    if (d.node.handle === $page?.params?.collection) {
      collection = d.node;
    }
  });
</script>

<svelte:head>
  <title>{collection?.handle} collection</title>
</svelte:head>

<div>
  {#if collection}
    <ul class="">
      {#each collection.products.edges as product, i (i)}
        <li>
          <div class="">
            <GridTile
              href={`/product/${product?.node?.handle}`}
              title={product?.node?.title}
              price={product?.node?.priceRange?.maxVariantPrice?.amount}
              currencyCode={product?.node?.priceRange?.maxVariantPrice?.currencyCode}
              imageSrc={product?.node?.images?.edges[0].node?.originalSrc}
            />
          </div>
        </li>
      {/each}
    </ul>
  {:else}
    <div>There are no products in this collection.</div>
  {/if}
</div>
