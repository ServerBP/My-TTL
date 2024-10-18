<script lang="ts">
  import { onMount } from 'svelte';

  // Set your target date here (example: July 4, 2025 00:00:00 UTC)
  const targetDate = new Date('2026-07-06T00:12:00Z').getTime();

  let days: number = 0;
  let hours: number = 0;
  let minutes: number = 0;
  let seconds: number = 0;
  let milliseconds: number = 0;

  function updateCountdown() {
    const now = new Date().getTime();
    const distance = targetDate - now;

    days = Math.floor(distance / (1000 * 60 * 60 * 24));
    hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
    seconds = Math.floor((distance % (1000 * 60)) / 1000);
    milliseconds = distance % 1000;
  }

  onMount(() => {
    updateCountdown();
    const interval = setInterval(updateCountdown, 10);
    return () => clearInterval(interval);
  });
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
</svelte:head>

<main>
  <h1>My TTL</h1>
  <div class="countdown">
    <div class="time-unit">
      <span class="value">{days}</span>
      <span class="label">Days</span>
    </div>
    <div class="time-unit">
      <span class="value">{hours}</span>
      <span class="label">Hours</span>
    </div>
    <div class="time-unit">
      <span class="value">{minutes}</span>
      <span class="label">Minutes</span>
    </div>
    <div class="time-unit">
      <span class="value">{seconds}</span>
      <span class="label">Seconds</span>
    </div>
    <div class="time-unit milliseconds">
      <span class="value">{milliseconds}</span>
      <span class="label">Milliseconds</span>
    </div>
  </div>
  <div class="explanation">
    <p>Soon™</p>
  </div>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'Roboto', sans-serif;
    background-color: #1a1a1a;
    color: #ffffff;
  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    min-height: 100vh;
    padding: 2rem;
    box-sizing: border-box;
  }

  h1 {
    font-size: 2.5rem;
    font-weight: 300;
    margin-bottom: 2rem;
  }

  .countdown {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .time-unit {
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #2a2a2a;
    border-radius: 8px;
    padding: 1rem;
    min-width: 100px;
  }

  .value {
    font-size: 3rem;
    font-weight: 700;
  }

  .label {
    font-size: 0.9rem;
    text-transform: uppercase;
    margin-top: 0.5rem;
  }

  .milliseconds {
    background-color: #3a3a3a;
  }

  .milliseconds .value {
    font-size: 2rem;
  }

  .explanation {
    max-width: 600px;
    text-align: center;
    margin-top: 2rem;
    font-size: 1rem;
    line-height: 1.5;
    color: #cccccc;
  }
</style>