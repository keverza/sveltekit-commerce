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
        <div class="a">{item.node.title}</div>
      </a>
    {/each}
  </div>
</div>

<style>
  @-webkit-keyframes scroll {
    0% {
      -webkit-transform: translateX(0);
      transform: translateX(0);
    }
    100% {
      -webkit-transform: translateX(calc(-250px * 7));
      transform: translateX(calc(-250px * 7));
    }
  }

  @keyframes scroll {
    0% {
      -webkit-transform: translateX(0);
      transform: translateX(0);
    }
    100% {
      -webkit-transform: translateX(calc(-250px * 7));
      transform: translateX(calc(-250px * 7));
    }
  }

  .slider::after {
    -webkit-transform: rotateZ(180deg);
    transform: rotateZ(180deg);
  }

  .slider .slide-track {
    -webkit-animation: scroll 40s linear infinite;
    animation: scroll 40s linear infinite;
  }
</style>
