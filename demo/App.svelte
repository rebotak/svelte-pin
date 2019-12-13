<script>
  import PinInput from 'svelte-pin-input';
  let value;
</script>

<style>
  main {
    padding: 30px 20px;
    max-width: 767px;
    margin: 0 auto;
  }
  h1 {
    margin: 16px 0;
  }
  p {
    margin-bottom: 5px;
  }
</style>

<main>
  <h1>Svelte pin input</h1>
  <p>example of usage:</p>
  <PinInput size={6} bind:pin={value} />
  PIN: {value}
</main>
