<script>
  export let items = [];
</script>

<div class="">
  <div class="">
    {#each items as item (item.node.id)}
      <a data-sveltekit-prefetch href={`/product/${item.node.handle}`} class="">
        <img
          alt={item.node.title}
          class=""
          decoding="async"
          loading="lazy"
          src={item.node.images.edges[0].node.originalSrc}
        />
        <div class="">{item.node.title}</div>
      </a>
    {/each}
  </div>
</div>

<style>
</style>
