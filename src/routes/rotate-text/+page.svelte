<script>
  let links = ['Lorem', 'Ipsum', 'Dolor', 'Sit', 'Amet']

  let menu
</script>

<nav bind:this={menu} class="rim">
  {#each links as link}
    <a href="/">
      <div>
        {#each link.split('') as l, i}
          <span style="--index: {i}">{l}</span>
        {/each}
      </div>
      <div>
        {#each link.split('') as l, i}
          <span style="--index: {i}">{l}</span>
        {/each}
      </div>
    </a>
  {/each}
</nav>

<style>
  nav {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-flow: column;
    align-items: center;
    justify-content: space-evenly;
    user-select: none;
  }
  nav a {
    position: relative;
  }
  a > div {
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
  }
  a > div span {
    will-change: transform;
    transform-style: preserve-3d;
    transition: .5s;
    transition-delay: calc(.05s * var(--index));
  }
  a > div:first-child span {
    transform: translate3d(0, 0, 0) rotateX(0);
  }
  a > div:last-child span {
    transform: translate3d(0, 100%, 0) rotateX(-90deg);
  }
  a:hover > div:first-child span {
    transform: translate3d(0, -100%, 0) rotateX(-90deg);
  }
  a:hover > div:last-child span {
    transform: translate3d(0, 0, 0) rotateX(0);
  } 
    span {
      text-transform: uppercase;
      cursor: pointer;
      pointer-events: none;
      line-height: .75;
      font-size: var(--font-size-1);
    }
      a {
        color: #000;
      }
</style>