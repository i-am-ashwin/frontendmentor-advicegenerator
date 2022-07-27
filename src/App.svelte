<script>
  	import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';
  const quote = 'Hello';
  const mobileImg = 'assets/images/pattern-divider-mobile.svg';
  const desktopImg = 'assets/images/pattern-divider-mobile.svg';
  const btnIcon = 'assets/images/icon-dice.svg';
  let adviceNumber = 404;
  let advice = 'Frontendmentor is fun';
  const getAdvice = async () => {
    fetch('https://api.adviceslip.com/advice')
      .then((response) => response.json())
      .then((data) => {
        adviceNumber = data.slip.id;
        advice = data.slip.advice;
      });
  };
onMount(async() => {
  await getAdvice();
});
  const handleClick = () => {
    getAdvice();
  };
</script>

<div class="container">
  <main class="card">
    {#key advice}
      <h1  class="title">Advice #{adviceNumber}</h1>
      <p in:fade class="advice-content">“{advice}”</p>
    {/key}
    <picture>
      <source srcset={mobileImg} media="(max-width: 550px)" />
      <img class="image" src={desktopImg} alt="divider" />
    </picture>
    <button on:click={handleClick} class="btn">
      <img src={btnIcon} alt="submit icon" />
    </button>
  </main>
</div>

<style>
  .container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }
  .card {
    width: 450px;
    border-radius: 20px;
    padding: 20px;
    background-color: var(--DarkGrayishBlue);
    height: auto;
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .btn {
    position: absolute;
    bottom: -25px;
    left: 0;
    right: 0;
    margin-left: auto;
    margin-right: auto;
    border-radius: 50px;
    width: 50px;
    height: 50px;
    border: 0;
    background-color: var(--NeonGreen);
    transition: all 150ms ease-in;
    cursor: pointer;
  }
  .btn:hover {
    box-shadow: 0 2px 30px var(--NeonGreen);
  }
  .btn:active {
    transform: scale(0.9);
  }
  .title {
    font-size: 1rem;
    font-weight: 800;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--NeonGreen);
  }
  .advice-content {
    text-align: center;
    font-size: 1.5rem;
    font-weight: 800;
    color: var(--LightCyan);
  }
  .image {
    margin-top: 20px;
    margin-bottom: 20px;
  }
</style>
