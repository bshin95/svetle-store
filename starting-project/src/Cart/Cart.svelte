<script>
  import { onDestory } from 'svelte'
  import CartItem from "./CartItem.svelte";
  import cartItems from './cart-store'
  import { timer } from '../timer-store'

  const unsubscribe = timer.subscribe(counter => {
    console.log('Cart:' + count)
  })

  // let items;

  // cartItems.subscribe(its => {
  //   // console.log(items)
  //   items = its
  // });

  onDestory(() =>{
    if (unsubscribe) {
      unsubscribe()
    }
  }) 
  //all this code above can be used with a svelte shortcode
  //this code can be rewritten as $cartItems, just like below in the html

  // export let items = [
  //   {
  //     id: "p1",
  //     title: "Test",
  //     price: 9.99
  //   },
  //   {
  //     id: "p2",
  //     title: "Test",
  //     price: 9.99
  //   }
  // ];
</script>

<style>
  section {
    width: 30rem;
    max-width: 90%;
    margin: 2rem auto;
    border-bottom: 2px solid #ccc;
  }

  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>

<section>
  <h1>Cart</h1>
  <ul>
    {#each $cartItems as item (item.id)}
      <CartItem id={item.id} title={item.title} price={item.price} />
    {:else}
      <p>No items in cart yet!</p>
    {/each}
  </ul>
</section>
<!-- variables starting with a $ allows svelte to assume it's a store, it will do everything behind the scenes by setting up a subscription, extracts data, and then uses the data. Svelte will also automatically unsubscribe the data. -->