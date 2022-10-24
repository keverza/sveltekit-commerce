<script>
  import GridTile from '$components/GridTile.svelte';

  export let products;
</script>

<div class="">
  <div class="">
    <GridTile
      priority="eager"
      href={`/product/${products[0].node.handle}`}
      title={products[0].node.title}
      price={products[0].node.priceRange.maxVariantPrice.amount}
      currencyCode={products[0].node.priceRange.maxVariantPrice.currencyCode}
      imageSrc={products[0].node.images.edges[0].node.originalSrc}
    />
  </div>
  <div class="">
    <div class="">
      <GridTile
        priority="eager"
        href={`/product/${products[1].node.handle}`}
        title={products[1].node.title}
        price={products[1].node.priceRange.maxVariantPrice.amount}
        currencyCode={products[1].node.priceRange.maxVariantPrice.currencyCode}
        imageSrc={products[1].node.images.edges[0].node.originalSrc}
      />
    </div>
    <div class="">
      <GridTile
        priority="eager"
        href={`/product/${products[2].node.handle}`}
        title={products[2].node.title}
        price={products[2].node.priceRange.maxVariantPrice.amount}
        currencyCode={products[2].node.priceRange.maxVariantPrice.currencyCode}
        imageSrc={products[2].node.images.edges[0].node.originalSrc}
      />
    </div>
  </div>
</div>
