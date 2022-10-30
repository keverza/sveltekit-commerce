<script>
  import { page } from '$app/stores';
  import { goto } from '$app/navigation';
  import Icons from './Icons.svelte';

  let value = $page.url.searchParams.get('q');

  async function submit(e) {
    let query = new URLSearchParams();
    if (value) {
      query.set('q', value);
    }
    await goto(`/search${query ? `?${query}` : ''}`, { keepfocus: true });
  }
</script>

<form on:submit|preventDefault={submit} class="">
  <div class="">
    <Icons strokeColor="#fff" type="search" />
  </div>
  <input
    id="searchInput"
    type="text"
    bind:value
    placeholder="Search for products..."
    autocomplete="off"
    class=""
  />
</form>

<style>
</style>
