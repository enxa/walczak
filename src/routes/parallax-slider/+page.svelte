<script>
  import { onMount } from "svelte";

  let links = [
    { id: 1, name: 'Lorem', image: '/images/1.jpg' },
    { id: 2, name: 'Ipsum', image: '/images/2.jpg' },
    { id: 3, name: 'Dolor', image: '/images/3.jpg' },
    { id: 4, name: 'Sit', image: '/images/4.jpg' },
    { id: 5, name: 'Amet', image: '/images/5.jpg' },
  ]

  let scrollY = 0
  let slider
  let slides = []
  
  let current = 0
  let target = 0
  let ease = 0.05

  let lerp = (start, end, easing) => start * (1 - easing) + end * easing

  $: if (slider) document.body.style.height = `${slider.getBoundingClientRect().width - (window.innerWidth - window.innerHeight)}px`

  let animate = () => {
    current = parseFloat(lerp(current, target, ease)).toFixed(2)
    target = scrollY
    slider.style.transform = `translateX(-${current}px)`
    slides = [...slider.querySelectorAll('.img')]
    slides.forEach((slide, id) => slide.style.transform = `translateX(${current / slides[0].getBoundingClientRect().width / (id * 0.7) * 70}px)`)
    requestAnimationFrame(animate)
  }

  onMount(() => animate())
</script>

<svelte:window bind:scrollY={scrollY} />

<section>
  <div class="slider" bind:this={slider}>
    <div class="slider-inner">
      {#each links as link}
        <div class="slide">
          <div class="img" style="background-image: url('{link.image}')"></div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  section {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
  }
    .slider {
      position: absolute;
      top: 0;
      left: 0;
      width: 2800px;
      height: 100%;
    }
      .slider-inner {
        position: absolute;
        top: 15%;
        width: 100%;
        height: 70%;
        display: flex;
        justify-content: space-around;
      }
        .slide {
          position: relative;
          width: 400px;
          height: 100%;
          overflow: hidden;
          background: black;
        }
          .img {
            position: absolute;
            left: -100px;
            width: 600px;
            height: 100%;
            background: no-repeat center center / cover;
          }

</style>