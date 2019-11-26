<script>
  import { onMount, afterUpdate } from "svelte";
  import { items } from "./data/data.json";

  import ModalCarrinhoComponent from "./components/ModalCarrinhoComponent.svelte";

  const name = "";
  let data = [];
  let imageIndice = 0;
  let showModalCarrinho = false;
  let itemsPendenting = [];

  onMount(async () => {
    data = items;
  });

  afterUpdate(() => {
    console.log(itemsPendenting);
  });

  function handleShowCarrinho() {
    showModalCarrinho = true;
    console.log(showModalCarrinho);
  }

  function handleAddItem(item) {
    itemsPendenting = [...itemsPendenting, item];
  }

  // setInterval(() => {
  //   if (imageIndice === 3) {
  //     return (imageIndice = 0);
  //   }
  //   return imageIndice++;
  // }, 2000);
</script>

<style>
  .border {
    border: 1px #ff3 solid !important;
  }
</style>

<div class="container">
  {#if name === 'Henrique'}
    <h1>Olá {name}</h1>
  {/if}

  <h1>Estudo Svelte</h1>
  <button
    class="btn btn-success"
    disabled={itemsPendenting == 0 ? 'true' : ''}
    on:click={handleShowCarrinho}>
    Carrinho
  </button>
  <ModalCarrinhoComponent show={showModalCarrinho} items={itemsPendenting} />

  <div class="row">
    {#each data as item}
      <div class="col-12 border my-3">
        <div class="row py-3">
          <div class="col-4">
            <img
              src={item.product.images[imageIndice]}
              alt={item.product.name}
              class="img-fluid" />
          </div>
          <div class="col-8 mt-3">
            <h5>{item.product.name}</h5>
            <p>Valor à vista:{item.product.price.value}</p>
            <p>Parcelado em até: {item.product.price.installments}</p>
            <p>Valor da parcela: {item.product.price.installmentValue}</p>
            <button
              class="btn btn-success"
              on:click={() => {
                itemsPendenting = [...itemsPendenting, item.product];
              }}>
              Adicionar
            </button>
          </div>
        </div>
      </div>
    {/each}
  </div>

</div>
