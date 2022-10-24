<script>
  import { page } from '$app/stores';
  import Icons from '$components/Icons.svelte';
  import { cartQuantity } from '../store';
  import SearchBar from '$components/SearchBar.svelte';
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  $: currentRoute = $page.url.pathname;

  let showMenu = false;

  let tabs = [
    { name: 'All', path: '/search' },
    { name: 'Featured', path: '/search/featured' },
    { name: 'Apparel', path: '/search/clothes' }
  ];
  function openCart() {
    showMenu = false;
    dispatch('openCart', true);
  }
</script>

<nav class="">
  <div class="">
    <div class="mr-4" class:active={currentRoute === '/'}>
      <a href="/" data-sveltekit-prefetch class="">
        <picture>
          <source srcset="/svelte_logo.png" type="image/png" />
          <img
            alt="Svelte Logo"
            class="h-[38] w-[32]"
            decoding="async"
            height={38}
            loading="eager"
            src="/svelte_logo.png"
            width={32}
          />
        </picture>
      </a>
    </div>
    <div class="hidden lg:flex">
      {#each tabs as tab, i (tab.name)}
        <div class:active={currentRoute === tab.path}>
          <a
            data-sveltekit-prefetch
            href={tab.path}
            class={`hover:opacity-100 px-2 py-1 text-white rounded-lg ${
              currentRoute === tab.path ? 'opacity-100' : 'opacity-75'
            }`}>{tab.name}</a
          >
        </div>
      {/each}
    </div>
  </div>
  <div class="">
    <SearchBar />
  </div>
  <div class="ml-auto flex items-center">
    <button on:click={openCart} class="">
      <Icons strokeColor="#fff" type="cart" />
      <div data-test="cart-quantity" class="">
        {$cartQuantity}
      </div>
    </button>
    <button
      on:click={() => {
        showMenu = true;
      }}
      aria-label="Open menu"
      class="lg:hidden"
    >
      <Icons type="menu" />
    </button>
  </div>
  {#if showMenu}
    <div
      on:click|self={() => {
        showMenu = false;
      }}
      class=""
    >
      <div class="">
        <div class="">
          <button
            aria-label="Close menu"
            on:click={() => {
              showMenu = false;
            }}
          >
            <Icons strokeColor="#fff" type="close" />
          </button>
          <button on:click={openCart} class="relative mr-4">
            <Icons strokeColor="#fff" type="cart" />
            <div class="">
              {$cartQuantity}
            </div>
          </button>
        </div>
        <div class="">
          {#each tabs as tab, i (tab.name)}
            <div
              class:active={currentRoute === tab.path}
              on:click={() => {
                showMenu = false;
              }}
            >
              <a
                data-sveltekit-prefetch
                href={tab.path}
                class={`hover:opacity-100 px-2 py-1 text-white font-bold text-xl rounded-lg ${
                  currentRoute === tab.path ? 'opacity-100' : 'opacity-75'
                }`}>{tab.name}</a
              >
            </div>
          {/each}
        </div>
      </div>
    </div>
  {/if}
</nav>
