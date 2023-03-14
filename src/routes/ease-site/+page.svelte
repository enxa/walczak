<script>
  import { onMount } from "svelte";

  let node
  
  let current = 0
  let target = 0
  let directionX
  let directionY

  let easing = 0.05
  
  let lerp = (start, end, easing) => start * (1 - easing) + end * easing

  let animate = () => {
    node.offsetWidth > node.offsetHeight ? 
    document.body.style.height = `${node.scrollWidth}px` : 
    document.body.style.height = `${node.scrollHeight}px`

    target = window.pageYOffset || document.documentElement.scrollTop
    current = lerp(current, target, easing)

    directionX = -1 * current
    directionY = 0 * current

    requestAnimationFrame(animate)
  }
  
  onMount(() => animate())
</script>

<section bind:this={node} style="transition: .25s all; position: fixed; transform: translate({directionX}px, {directionY}px)">
  <div style="width: 100vw; height: 100vh" class="rim">
    <h4>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Ut ipsa sint sequi sit accusamus minima nesciunt, cumque laboriosam nihil nisi id provident beatae ab aut quibusdam sed nemo molestias praesentium?</h4>
  </div>
  <div style="width: 50vw; height: 200vh" class="rim">
    <h4>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Quae vel mollitia qui itaque impedit non quisquam excepturi laudantium voluptate pariatur, possimus eligendi assumenda voluptatibus modi rem reprehenderit repellendus. Veniam, est!</h4>
  </div>
</section>

<style>
  section {
    display: flex;
  }
</style>