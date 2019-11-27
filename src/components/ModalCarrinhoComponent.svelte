<script>
  export let show;
  export let items;
  export let handleBack;
</script>

<style>

</style>

{#if show}
  <div class="container mt-5">
    <div class="jumbotron">
      <button on:click={handleBack}>Voltar</button>
      <div class="border">
        {#each items as item}
          <p>{item.name}</p>
        {/each}
      </div>
    </div>
  </div>
{/if}
