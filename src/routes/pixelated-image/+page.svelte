<script>
  import { browser } from '$app/environment'

  let links = [
    { id: 1, name: 'Lorem', image: '/images/1.jpg' },
    { id: 2, name: 'Ipsum', image: '/images/2.jpg' },
    { id: 3, name: 'Dolor', image: '/images/3.jpg' },
    { id: 4, name: 'Sit', image: '/images/4.jpg' },
    { id: 5, name: 'Amet', image: '/images/5.jpg' },
  ]

  let canvas
  let currentImg
  
  let percent = 0
  let target = 0

  let targetX = 0
  let targetY = 0
  let currentX = 0
  let currentY = 0

  let easing = 0.05

  let lerp = (start, end, easing) => start * (1 - easing) + end * easing

  let handleMouseover = e => {
    [...e.target.parentNode.children].forEach(link => link.classList.remove('active'))
    e.target.classList.add('active')
    currentImg = e.target.nextElementSibling
    target = 1
  }

  let handleMouseleave = e => {
    [...e.target.children].forEach(link => link.classList.add('active'))
    target = 0
  }

  let handleMousemoveWindow = e => {
    targetX = e.clientX
    targetY = e.clientY
  }

  let animate = () => {
    if (currentImg) {
      let { width, height } = currentImg.getBoundingClientRect()
      currentX = lerp(currentX, targetX, easing)
      currentY = lerp(currentY, targetY, easing)

      canvas.style.transform = `translate3d(${currentX - (width / 2)}px, ${currentY - (height / 2)}px, 0)`
      canvas.width = width * window.devicePixelRatio
      canvas.height = height * window.devicePixelRatio

      let ctx = canvas.getContext('2d')
      ctx.imageSmoothingEnabled = false   // pixelate by disabling the smoothing

      if (percent <= target) percent += .01
      if (percent >  target) percent -= .01

      if (percent >= 1) ctx.drawImage(currentImg, 0, 0, width, height)
      if (percent <  1) ctx.drawImage(currentImg, 0, 0, width * percent, height * percent)
      if (percent <  1 && canvas.width !== 0 && canvas.height !== 0) ctx.drawImage(canvas, 0, 0, width * percent, height * percent, 0, 0, width, height)
    }

    if (browser) requestAnimationFrame(animate)
  }
  animate()

</script>

<svelte:window on:mousemove={handleMousemoveWindow}/>

<main>
  <canvas bind:this={canvas}></canvas>
  <section>
    <div>
      <ul>
        {#each links as link, i}
          <li on:mouseover={handleMouseover}  on:mouseleave={handleMouseleave} on:focus={handleMouseover} value={i} class:active={false}>
            <a href="/#" style="pointer-events: none;">{link.name}</a>
          </li>
          <img src={link.image} alt={'image' + i} class="project-image">
        {/each}
      </ul>
    </div>
  </section>
</main>

<style>
  main {
    height: 100vh;
  }
    canvas {
      position: fixed;
      z-index: 10;
      pointer-events: none;
    }

    section {
      position: relative;
      padding: 10vh 10vw;
      height: 100vh;
      width: 100%;
    }
      div {
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
      }
        ul {
          display: inline-flex;
          flex-direction: column;
          justify-content: space-evenly;
        }
          li {
            display: inline-block;
            position: relative;
            text-align: center;
            cursor: pointer;
            font-size: var(--font-size-1);
            opacity: 0.25;
            z-index: 0;
          }
            a {
              color: #000;
            }

          .active {
            opacity: 1;
            z-index: 10;
          }
    
    .project-image {
      opacity: 0;
      position: absolute;
      pointer-events: none;
      user-select: none;
    }


</style>
