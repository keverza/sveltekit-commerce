<script>
  import GridTile from '$components/GridTile.svelte';
  import DescriptionToggle from '$components/DescriptionToggle.svelte';
  import Icons from '$components/Icons.svelte';
  import { getCartItems } from '../../../store.js';

  /** @type {import('./$types').PageData} */
  export let data;

  let selectedOptions = {};
  let cartLoading = false;
  let currentImageIndex = 0;

  $: highlightedImageSrc = data?.body?.product?.images?.edges[currentImageIndex]?.node?.originalSrc;

  data?.body?.product?.options.forEach((option) => {
    selectedOptions = { ...selectedOptions, [option.name]: option.values[0] };
  });

  function changeHighlightedImage(direction) {
    if (direction === 'next') {
      if (currentImageIndex + 1 < data?.body?.product?.images?.edges.length) {
        currentImageIndex = currentImageIndex + 1;
      } else {
        currentImageIndex = 0;
      }
    } else {
      if (currentImageIndex === 0) {
        currentImageIndex = data?.body?.product?.images?.edges.length - 1;
      } else {
        currentImageIndex = currentImageIndex - 1;
      }
    }
  }

  async function addToCart() {
    cartLoading = true;
    let variantId;
    let cartId;

    if (typeof window !== 'undefined') {
      cartId = JSON.parse(localStorage.getItem('cartId'));
    }

    data.body.product.variants.edges.forEach((variant) => {
      let result = variant.node.selectedOptions.every((option) => {
        return selectedOptions[option.name] === option.value;
      });
      if (result) {
        variantId = variant.node.id;
      }
    });

    await fetch('/cart.json', {
      method: 'PATCH',
      body: JSON.stringify({ cartId: cartId, variantId: variantId })
    });
    // Wait for the API to finish before updating cart items
    await getCartItems();

    cartLoading = false;
  }
</script>

<svelte:head>
  <title>{data.body.product.title}</title>
</svelte:head>

<div>
  {#if data.body.product}
    <div class="">
      <div class="">
        {#key highlightedImageSrc}
          <div class="">
            <GridTile
              title={data.body.product.title}
              price={data.body.product.priceRange.maxVariantPrice.amount}
              currencyCode={data.body.product.priceRange.maxVariantPrice.currencyCode}
              imageSrc={highlightedImageSrc}
            />
            {#if data.body.product?.images?.edges.length > 1}
              <div class="">
                <button
                  on:click={() => {
                    changeHighlightedImage('back');
                  }}
                  class=""><Icons type="arrowLeft" /></button
                >
                <button
                  on:click={() => {
                    changeHighlightedImage('next');
                  }}
                  class=""><Icons type="arrowRight" /></button
                >
              </div>
            {/if}
          </div>
        {/key}
        <div class=" ">
          {#each data.body.product.images.edges as variant, i}
            <div
              on:click={() => {
                currentImageIndex = i;
              }}
              class=""
            >
              <GridTile imageSrc={variant.node.originalSrc} removeLabels={true} />
            </div>
          {/each}
        </div>
      </div>
      <div class="">
        {#each data.body.product.options as option}
          <div class="">
            <div class="">{option.name}</div>
            <div class="">
              {#each option.values as value}
                <button
                  on:click={() => {
                    selectedOptions = { ...selectedOptions, [option.name]: value };
                  }}
                  class={`${value.length <= 3 ? 'w-12' : 'px-2'} ${
                    selectedOptions[option.name] === value ? 'opacity-100' : 'opacity-60'
                  } `}
                >
                  {value}
                </button>
              {/each}
            </div>
          </div>
        {/each}
        <p class="">{data.body.product.description}</p>
        <div class="">
          <div class="">
            <div class="mr-1">
              <Icons type="star" />
            </div>
            <div class="mr-1">
              <Icons type="star" />
            </div>
            <div class="mr-1">
              <Icons type="star" />
            </div>
            <div class="mr-1">
              <Icons type="star" />
            </div>
            <div class="mr-1 opacity-50">
              <Icons type="star" />
            </div>
          </div>
          <div class="">36 Reviews</div>
        </div>
        <button on:click={addToCart} class="">
          <span>Add To Cart</span>
          {#if cartLoading}
            <div class="">
              <div />
              <div />
              <div />
              <div />
            </div>
          {/if}
        </button>
        <DescriptionToggle
          title="Care"
          description="This is a limited edition production run. Printing starts when the drop ends."
        />
        <DescriptionToggle
          title="Details"
          description="This is a limited edition production run. Printing starts when the drop ends. Reminder: Bad Boys For Life. Shipping may take 10+ days due to COVID-19."
        />
      </div>
    </div>
    <div class="">
      <div class="">Related Products</div>
      <ul class="">
        {#each data.body.featuredProducts as product, i (product.node.id)}
          <li>
            <div class="">
              <GridTile
                removeLabels={true}
                imageSrc={product.node.images.edges[0].node.originalSrc}
                href={`/product/${product.node.handle}`}
              />
            </div>
          </li>
        {/each}
      </ul>
    </div>
  {/if}
</div>

<style>
</style>
