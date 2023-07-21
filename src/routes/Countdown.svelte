<!-- src/Countdown.svelte -->
<script>
  let timeLeft = 3; // Set the initial countdown time in seconds
  let timer = null;

  function playSound() {
    let audio = new Audio("/sounds/beep.mp3");
    audio.play();
  }

  function resetCountdown() {
    timeLeft = 3;
  }

  function startCountdown() {
    if (timer) return; // Prevent multiple timers from running
    timer = setInterval(() => {
      timeLeft -= 1;
      if (timeLeft === 0) {
        clearInterval(timer);
        timer = null;
        playSound();
      }
    }, 1000);
  }
</script>

<main>
  <input
    placeholder="Set Time"
    value={timeLeft}
    on:input={(i) => (timeLeft = i.target.value)}
  />
  <h1>{timeLeft}s</h1>
  {#if timeLeft === 0}
    <button on:click={resetCountdown}>Reset</button>
  {:else}
    <button on:click={startCountdown}>Start Countdown</button>
  {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    font-size: 3em;
  }

  button {
    padding: 10px 20px;
    font-size: 1em;
  }
</style>
