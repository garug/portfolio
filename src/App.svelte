<script>
  import { onMount } from "svelte";

  const socialMedia = [
    {
      classIcon: "fab fa-facebook-f",
      link: "http://fb.com/allefgarug",
    },
    {
      classIcon: "fab fa-linkedin-in",
      link: "https://www.linkedin.com/in/allefsantana/",
    },
    {
      classIcon: "fab fa-github",
      link: "https://github.com/garug",
    },
  ];

  let stars = new Array(90).fill().map((_, i) => {
    return {
      x: randomIntFromInterval(-2, 95),
      y: randomIntFromInterval(-5, 95),
      rate: Math.random(),
      opacity: 0,
    };
  });

  const updateStars = () => {
    stars = stars.map((star) => {
      const isUpdated = Math.random() > 0.5;
      star.rate = Math.random();
      if (isUpdated && star.opacity >= 1) {
        star.opacity = 0;
        star.x = randomIntFromInterval(-2, 95);
        star.y = randomIntFromInterval(-5, 95);
      } else {
        star.opacity += Math.random();
      }
      return star;
    });
  };

  onMount(() => {
    updateStars();
    setTimeout(() => updateStars(), 1);
    setTimeout(() => updateStars(), 2);
    setTimeout(() => updateStars(), 3);
    setInterval(() => updateStars(), 3000);
    // let frame;

    // function loop() {
    //   frame = requestAnimationFrame(loop);

    //     stars = stars.map((emoji) => {
    //       const tick = Math.random() * 100;
    //       if (emoji.opacity >= 1) {
    //         emoji.opacity = -0.1;
    //         emoji.x = Math.random() * 100;
    //         emoji.y = Math.random() * 100;
    //       } else {
    //         emoji.opacity += tick / 75025;
    //       }
    //       return emoji;
    //     });
    // }

    // loop();

    // return () => cancelAnimationFrame(frame);
  });

  function randomIntFromInterval(min, max) {
    return Math.floor(Math.random() * (max - min + 1) + min);
  }

  let m = { x: 0, y: 0 };
  let paused = false;
  const music = "media/hase-hours.mp3";
</script>

<style>
  main {
    height: 100%;
    background-color: #2f2f3d;

    font-family: "Maven Pro", sans-serif;

    display: flex;
    align-items: center;
    justify-content: center;
  }

  main .content {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    z-index: 1;
  }

  main p {
    color: #fff;
    font-size: calc(12px + 2vmin);
    font-weight: 600;
    overflow: hidden;
  }

  .heading {
    color: #fff;
    font-size: 16vmin;
    line-height: 16vmin;
    font-weight: 600;
    margin-bottom: 5vmin;
  }

  .social-container {
    margin-top: 5vmin;
    margin-bottom: 5vmin;
    display: flex;
  }

  .social {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid #fff;
    width: 50px;
    height: 50px;
    margin-right: 5px;
    color: #fff;
    transition: all ease-in-out 0.25s;
  }

  .social:hover {
    background: #c03f92;
    border-color: #c03f92;
    transform: translateY(-2px);
  }

  .stars {
    position: absolute;
    overflow: hidden;
    height: 100vh;
    width: 100vw;
  }

  .star {
    position: absolute;
    font-size: 5vw;
    color: #fff;
    font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
    opacity: 0;
  }
</style>

<main on:mousemove={(e) => (m = { x: e.clientX, y: e.clientY })}>
  <div class="stars">
    {#each stars as c}
      <span
        class="star"
        style="transition: all ease {c.rate * 100}s, opacity linear 1s; opacity:
        {c.opacity}; left: {c.x}%; top: {c.y}%; transform: scale({randomIntFromInterval(2, 8) / 100})">
        <svg height="100" width="100">
          <circle cx="50" cy="50" r="40" stroke-width="3" fill="#fff" />
        </svg>
      </span>
    {/each}
  </div>
  <div class="content">
    <p>Oi pessoa, eu sou o</p>
    <h1
      class="heading"
      style="text-shadow: {m.x / 50 - 25}px {m.y / 25 - 25}px #c03f92;
      transform: translateY({(m.y / 100 - 25) * -1}px) translateX({(m.x / 100 - 50) * -1}px)">
      garug
    </h1>
    <p>E essas são minhas redes sociais</p>
    <div class="social-container">
      {#each socialMedia as { classIcon, link }}
        <a class="social" href={link}>
          <i class={classIcon} />
        </a>
      {/each}
    </div>
    <!-- svelte-ignore a11y-media-has-caption -->
    <audio autoplay="true" bind:paused controls="controls" loop="true">
      <source src={music} type="audio/mp3" />
      seu navegador não suporta HTML5
    </audio>
  </div>
</main>
