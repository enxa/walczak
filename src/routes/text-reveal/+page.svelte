<script>
  import { onMount } from "svelte";

  let node
  let h1Elements
  let randomChars = [...'!@#$%^&*()_+-={}[]<>qwertyuiopasdfghjklzxcvbnm'.split('')]

  $: if (node) h1Elements = [...node.querySelectorAll('h2')]

  $: console.log(h1Elements)
  $: console.log(randomChars)

  // $: console.log(specialChars)
</script>

<section bind:this={node} class="rim">
  <div>
    <h2>Lorem Ipsum</h2>
  </div>
  <div>
    <h2>Et Dolorem</h2>
  </div>
  <div>
    <h2>Sit Amet</h2>
  </div>
</section>

<style>
  div {
    height: 100vh;
    display: grid;
    place-items: center;
  }
    h2 {
      opacity: 0;
      transition: .4s all ease-in-out;
    }
</style>