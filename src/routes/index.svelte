<script>
  import CountDown from "../components/CountDown.svelte";
  import Header from "../components/Header.svelte";
  import Image from "../components/Image.svelte";

  let audio;
  function timerEnds(e) {
    audio.play();
  }
</script>

<main class="container">
  <section class="d-flex flex-column align-items-center">
    <div class="col-md-5">
      <Header />
      <CountDown on:end={timerEnds}/>
      <Image />
    </div>
  </section>
  <audio bind:this={audio}>
    <source src="sound.wav" />
  </audio>
</main>


<style>
  :global(body) {
    font-family: "Lato", sans-serif;
  }
</style>
