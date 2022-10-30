<script>
  import Icons from '$components/Icons.svelte';
  import { fade } from 'svelte/transition';

  export let title;
  export let description;

  let toggle = false;
</script>

<button
  on:click={() => {
    toggle = !toggle;
  }}
  class=" "
>
  <div class={`opacity-50 h-6 w-6 rotate ${toggle ? 'down' : ''}`}>
    <Icons type="caretRight" strokeColor="#fff" />
  </div>
  <div class="">
    <div class="m">{title}</div>
    {#if toggle}
      <div transition:fade={{ duration: 300 }}>{description}</div>
    {/if}
  </div>
</button>

<style>
</style>
