<script>
  import { onMount } from "svelte";
  const KEYBOARD = {
    BACKSPACE: 8,
    DELETE: 46,
    ANDROID_BACKSPACE: 229,
  };
  let inputs = [];
  export let pin = '';
  export let size = 6;
  export let disabled = false;

  const isKeyDelete = (key) => {
    return key === KEYBOARD.BACKSPACE
      || key === KEYBOARD.DELETE
      || key === KEYBOARD.ANDROID_BACKSPACE;
  };
  const onKeyDown = (e, currentIndex) => {
    const current = document.activeElement;
    let isDigit = new RegExp(/^\d+$/);
    if (isKeyDelete(e.keyCode) && currentIndex === 0) {
      return pin = '';
    } else if (isKeyDelete(e.keyCode) && currentIndex !== 0) {
      pin = pin.slice(0, currentIndex - 1);
      const newIndex = Math.max(0, currentIndex - 1);
      return inputs[newIndex].focus();
    }

    if (isDigit.test(e.key)) {
      pin = pin.slice(0, currentIndex);
      pin += e.key;
      current.blur();
      if (currentIndex !== inputs.length - 1 || isKeyDelete(e.keyCode)) {
        const newIndex = (currentIndex + 1) % inputs.length;
        inputs[newIndex].focus();
      }
    }
  };
</script>

<style>
  .pin-input {
    width: 100%;
    position: relative;
    margin: 0 auto;

    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: row;
    flex-wrap: nowrap;
  }
  input {
    width: 32px;
    height: 40px;
    border: none;
    border-bottom: 1px solid black;
    border-radius: 0;
    margin: 0 4px;
    text-align: center;
    background: transparent;
  }
  input:focus {
    outline: none;
  }
</style>

<div class="pin-input">
  {#if size}
    {#each Array(size) as o, i}
      <input
        bind:this={inputs[i]}
        on:keydown|preventDefault={(event) => onKeyDown(event, i)}
        class="pin-item"
        disabled={disabled}
        value={pin[i] || ''}
        maxLength="1"
        type="tel"
        pattern="\d{1}"
        maxlength="1"
        placeholder="" />
    {/each}
  {/if}
</div>
