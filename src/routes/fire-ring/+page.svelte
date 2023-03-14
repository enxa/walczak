<script>
  let baseFrequency = 0.009
  let numOctaves = 5
  let seed = 2
  let duration = 60
  let aniamteValues = '0.02;0.005;0.02'
  let repeatCount = 'indefinite'
  let displacementMapScale = 30
</script>

<section>
  <div class="ring"></div>
  <svg>
    <filter id="wavy">
      <feTurbulence x="0" y="0"                                                                                                                                                                                                                                         
        baseFrequency={baseFrequency} 
        numOctaves={numOctaves} 
        seed={seed}>
        <animate attributeName="baseFrequency" 
          dur={duration + 's'} 
          values={aniamteValues} 
          repeatCount={repeatCount}
        >
      </feTurbulence>
      <feDisplacementMap in="SourceGraphic" scale={displacementMapScale}>
    </filter>
  </svg>

  <form>
    <label class="rim">
      <input type="range" min="0" max="10" bind:value={baseFrequency}> frequency
    </label>
    <label class="rim">
      <input type="range" min="0" max="10" bind:value={numOctaves}> octaves
    </label>
    <label class="rim">
      <input type="range" min="0" max="10" bind:value={seed}> seed
    </label>
    <label class="rim">
      <input type="range" min="0" max="100" bind:value={duration}> duration
    </label>
    <label class="rim">
      <input type="range" min="0" max="100" bind:value={displacementMapScale}> displacement
    </label>
  </form>
</section>

<style>
  section {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #000;
    color: #fff;
  }
    .ring {
      position: relative;
      width: 600px;
      height: 600px;
      filter: url(#wavy) blur(1px)
    }

    .ring::before {
      content: '';
      position: absolute;
      top: 100px;
      left: 100px;
      right: 100px;
      bottom: 100px;
      border: 10px solid #fff;
      border-radius: 50%;
      box-shadow: 0 0 50px #fff, 
            inset 0 0 50px #fff;
      -webkit-box-reflect: below 10px linear-gradient(transparent, transparent, #0002);
      animation: animate 5s linear infinite;
    }
    .ring::after {
      content: '';
      position: absolute;
      top: 100px;
      left: 100px;
      right: 100px;
      bottom: 100px;
      border: 10px solid #fff;
      border-radius: 50%;
      box-shadow: 0 0 50px #fff, 
            inset 0 0 50px #fff;
      -webkit-box-reflect: below 10px linear-gradient(transparent, transparent, #0002);
      animation: animate 5s linear infinite;
    }

    svg {
      width: 0;
      height: 0;
    }

@keyframes animate {
  0% {
    box-shadow: 0 0 50px #fff, 
          inset 0 0 50px #fff;
    filter: hue-rotate(0deg)
  }
  20% {
    box-shadow: 0 0 60px #fff, 
          inset 0 0 60px #fff;
    filter: hue-rotate(0deg)
  }
  40% {
    box-shadow: 0 0 40px #fff, 
          inset 0 0 40px #fff;
    filter: hue-rotate(0deg)
  }
  60% {
    box-shadow: 0 0 80px #fff, 
          inset 0 0 80px #fff;
    filter: hue-rotate(0deg)
  }
  80% {
    box-shadow: 0 0 100px #fff, 
          inset 0 0 100px #fff;
    filter: hue-rotate(0deg)
  }
  100% {
    box-shadow: 0 0 50px #fff, 
          inset 0 0 50px #fff;
    filter: hue-rotate(360deg)
  }
}
</style>