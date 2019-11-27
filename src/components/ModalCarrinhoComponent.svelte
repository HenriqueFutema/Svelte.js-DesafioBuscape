<script>
  import { onMount } from "svelte";

  export let show;
  export let items;
  export let handleBack;
  export let handleUpdateData;

  function handleRemoveItem(item) {
    const index = items.indexOf(item);
    items = [...items.slice(0, index), ...items.slice(index + 1)];
    console.log(items);
    handleUpdateData(items);
  }
</script>

<style>

</style>

{#if show}
  <div class="container mt-5">
    <div class="jumbotron">
      <h5>
        Carrinho
        <button on:click={handleBack}>Voltar</button>
      </h5>

      <div class="border">
        {#each items as item}
          <div class="row py-3">
            <div class="col-4">
              <button
                class="btn btn-danger btn-rounded"
                on:click={() => handleRemoveItem(item)}>
                X
              </button>
              <img
                src={item.product.images[0]}
                alt={item.product.name}
                class="img-fluid" />
            </div>
            <div class="col-8 mt-3">
              <h5>{item.product.name}</h5>
              <p>Valor à vista:{item.product.price.value}</p>
              <p>Parcelado em até: {item.product.price.installments}</p>
              <p>Valor da parcela: {item.product.price.installmentValue}</p>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
{/if}
