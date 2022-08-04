<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  const totalSeconds = 20;
  let secondLeft = totalSeconds;
  $: process = ((totalSeconds - secondLeft) / totalSeconds) * 100;
  let isRunning = false;

  // paly audio after 1 second
  let audio;
  function playAudio(e) {
    audio.play();
  }

  // cound down function
  const startCountDown = () => {
    isRunning = true;
    const timer = setInterval(() => {
      secondLeft -= 1;
      playAudio();

      if (secondLeft == 0) {
        clearInterval(timer);
        isRunning = false;
        secondLeft = totalSeconds;
        dispatch("end");
      }
    }, 1000);
  };
</script>

<article>
  <h3>Time Left: {secondLeft}</h3>
  <div class="my-progress-bar">
    <div class="my-progress" style="width: {process}%" />
  </div>
  <button disabled={isRunning} class="start" on:click={startCountDown}>
    Start
  </button>
<!-- audio -->
  <audio bind:this={audio}>
    <source src="1.mp3" />
  </audio>
</article>



<style>
  h3 {
    font-weight: 700;
    color: #000;
  }
  .my-progress-bar {
    border: solid rgb(194, 194, 194) 1px;
  }
  .my-progress {
    height: 30px;
    background-color: rgb(77, 199, 55);
    /* width: 10%; */
  }
  .start {
    display: block;
    background-color: rgb(154, 73, 73);
    width: 100%;
    margin: 10px 0;
    border: none;
    color: #fff;
    outline: none;
    padding: 15px 32px;
    text-align: center;
    margin-bottom: 30px;
    margin-top: 30px;
  }
  .start[disabled] {
    background-color: rgb(194, 194, 194);
    cursor: not-allowed;
  }
</style>
