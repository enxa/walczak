<script>
  import { browser } from '$app/environment'

  let links = ['Lorem', 'Ipsum', 'Dolor', 'Sit', 'Amet']

  let toggle = false
  
  let y = 0
  let c = -100

  let path = `M 0 0 L 0 0 100 0 100 0 C 50 100, 50 100, 0 100`
          // `M 0 100 L 0 100 100 100 100 100 C 50 100, 50 100, 0 100`
  let lerp = (start, end, easing) => start * (1 - easing) + end * easing
  
  let animate = () => {
    if (toggle) {
      y = lerp(y, 100, .050).toFixed(2)
      c = lerp(c, 100, .075).toFixed(2)
    } else {
      y = lerp(y, 0, .050).toFixed(2)
      c = lerp(c, 0, .075).toFixed(2)
    }
    path = `M 0 ${y} L 0 0 100 0 100 ${y} C 50, ${c} 50 ${c}, 0 ${y}`

    if (browser) requestAnimationFrame(animate)
  }
  animate()

</script>

<section>
  <header>
    <div class="menu-toggle" on:click={() => toggle = !toggle}>
      MENU
    </div>
  </header>

  <nav>
    <svg class="transition" viewBox="0 0 100 100" preserveAspectRatio="none">
      <path class="path" fill="#000" d={path}></path>
    </svg>

    <ul class:active={toggle}>
      {#each links as link}
        <li><a href="/">{link}</a></li>
      {/each}
    </ul>
  </nav>
</section>

<style>
    header {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 50px;
      z-index: 10;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      padding: 0 2vw;
      mix-blend-mode: difference;
    }
    .menu-toggle {
      position: relative;
      display: flex;
      flex-direction: column;
      cursor: pointer;
      justify-content: space-evenly;
      color: gray;
    }

    nav {
      position: fixed;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }

      .transition {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
      }
        ul {
          position: relative;
          transition: .5s;
          height: 300px;
          display: flex;
          flex-direction: column;
          justify-content: space-between;
          align-items: space;
          opacity: 0;
          pointer-events: none;
        }

        ul.active {
          opacity: 1;
          pointer-events: all;
        }

          a {
            color: #fff;
          }
</style>