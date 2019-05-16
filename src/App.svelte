<script>
  import Product from "./Product.svelte";
  import Button from "./Button.svelte";
  import Cart from "./Cart.svelte";

  export let name;

  let title = "";
  let price = 0;
  let description = "";

  let products = [];
  let cartItems = [];

  function setTitle(event) {
    title = event.target.value;
  }

  function createProduct() {
    const newProduct = {
      title,
      price,
      description
    };
    products = products.concat(newProduct);
  }

  function addToCart(event) {
    const selectedTitle = event.detail;
    cartItems = cartItems.concat({
      ...products.find(prod => prod.title === selectedTitle)
    });
  }
</script>

<style>
  h1 {
    color: purple;
    text-align: center;
  }
  section {
    width: 30rem;
    margin: auto;
  }
  label,
  input {
    width: 100%;
  }
</style>

<h1>This is a {name} for Svelte</h1>

<section>
  <Cart items={cartItems} />
</section>

<hr />

<section>
  <div>
    <label for="title">Title</label>
    <input
      type="text"
      name="title"
      id="title"
      value={title}
      on:input={setTitle} />
    <!-- value={title}
      on:input={setTitle} puede ser remplazado por bind:value={title} -->
  </div>
  <div>
    <label for="price">Price</label>
    <input type="number" name="price" id="price" bind:value={price} />
  </div>
  <div>
    <label for="description">Description</label>
    <textarea
      name="description"
      id="description"
      cols="30"
      rows="10"
      bind:value={description} />
  </div>

  <Button on:click={createProduct}>Create Product</Button>

</section>

<section>
  {#if products.length === 0}
    <p>No products</p>
  {:else}
    {#each products as product}
      <Product
        productTitle={product.title}
        productPrice={product.price}
        productDescription={product.description}
        on:addCart={addToCart} />
    {/each}
  {/if}
</section>
