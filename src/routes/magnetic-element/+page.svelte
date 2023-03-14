<script>
  let link
  let x
  let y

  let handleMousemove = e => {
    let { left, top, width, height } = link.getBoundingClientRect()
    x = e.clientX - left - width / 2
    y = e.clientY - top - height / 2
  }
  let handleMouseout = e => {
    x = 0
    y = 0
  }
</script>

<section>
  <a href="/#" bind:this={link} on:mousemove={handleMousemove} on:mouseout={handleMouseout} on:blur={handleMouseout}>
    <span style="will-change: transform; transition: transform .5s ease-out; transform: translate({x * .5}px, {y * .5}px);">Lorem ipsum</span>
  </a>
</section>

<style>
  section {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
    a {
      position: relative;
      text-align: center;
    }
      span {
        position: relative;
        display: inline-block;
        color: #000;
        font-size: var(--font-size-2);
        padding: var(--font-size-2);
        margin: var(--font-size-2);
      }
</style>
