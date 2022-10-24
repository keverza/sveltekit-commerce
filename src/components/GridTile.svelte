<script>
  export let title = '';
  export let removeLabels = false;
  export let imageSrc;
  export let price = '';
  export let currencyCode = '';
  export let href = '';
  export let priority = 'lazy';

  let hover = false;
</script>

<div
  on:mouseenter={() => {
    hover = true;
  }}
  on:mouseleave={() => {
    hover = false;
  }}
  class=""
>
  <a data-test="grid-tile" {href} data-sveltekit-prefetch class="">
    <img
      alt={title}
      class={`w-full md:w-1/2 lg:w-full flex-none transition duration-300 ease-in-out ${
        hover ? 'scale-110' : ''
      }`}
      fetchpriority={priority === 'eager' ? 'high' : 'low'}
      decoding="async"
      loading={priority}
      src={imageSrc}
    />
    {#if !removeLabels}
      <div class="">
        <div class="">
          {title}
        </div>
        <div class="">
          ${price}
          {currencyCode}
        </div>
      </div>
    {/if}
  </a>
</div>
