<svelte:head>
  <title>Home</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<nav>
  <a href="/responsive-typography">Responsive typography</a>
  <a href="/ease-site">Site easing</a>
  <a href="/magnetic-element">Magnetic element</a>
  <a href="/rotate-text">Text rotate</a>
  <a href="/curve-menu">Menu curved</a>
  <a href="/pixelated-image">Pixelated image effect</a>
  <a href="/fire-ring">Fire ring</a>
  <!-- <a href="/scroll-3d-effect">Scroll 3d effect</a> -->
  <a href="/parallax-slider">Parallax slider</a>
</nav>

<style>
  :global(body) {
    width: 100%;
    height: 100vh;
  }
  nav {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    overflow: hidden;
  }
</style>