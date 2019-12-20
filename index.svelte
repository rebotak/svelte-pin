<script>
  import { onMount } from "svelte";

  const KEYBOARD = {
    BACKSPACE: 8,
    DELETE: 46,
    ANDROID_BACKSPACE: 229
  };

  let inputs = [0];
  let pins = {};

  export let pin;
  export let size = 6;

  onMount(async () => {
    inputs = await createArray(size);
    pins = await createValueSlot(inputs);
    pin = calcPin(pins);
    document.getElementById("pin0").focus();
  });

  const calcPin = pins => {
    if (Object.values(pins).length) {
      return Object.values(pins).join("");
    } else return "";
  };

  const changeHandler = function(e, i) {
    let nextPin = e.target.nextElementSibling;
    let prevPin = e.target.previousElementSibling;
    let regx = new RegExp(/^\d+$/);
    if (
      (e.keyCode == KEYBOARD.BACKSPACE ||
        e.keyCode == KEYBOARD.DELETE ||
        e.keyCode == KEYBOARD.ANDROID_BACKSPACE) &&
      !prevPin
    ) {
      pins[i] = "";
    } else if (
      (e.keyCode == KEYBOARD.BACKSPACE ||
        e.keyCode == KEYBOARD.DELETE ||
        e.keyCode == KEYBOARD.ANDROID_BACKSPACE) &&
      prevPin
    ) {
      pins[i] = "";
      prevPin.focus();
    } else if (nextPin) {
      if (regx.test(e.key)) {
        pins[i] = e.key;
      } else {
        return;
      }
      setTimeout(() => {
        nextPin.focus();
      }, 0);
    } else {
      if (regx.test(e.key)) {
        pins[i] = e.key;
      } else {
        return;
      }
    }

    pin = calcPin(pins);
  };
  const createArray = size => {
    return new Array(size);
  };
  const createValueSlot = arr => {
    return arr.reduce((obj, item) => {
      return {
        ...obj,
        [item]: ""
      };
    }, {});
  };
</script>

<style>
  .pin-input {
    position: relative;
    margin: 0 auto;
    align-items: center;
    justify-content: center;
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
  }
  input {
    width: 32px;
    -webkit-text-security: disc;
    border: none;
    text-align: center;
    border-bottom: 1px solid black;
    margin: 0 4px;
    border-radius: 0;
    height: 40px;
    background: transparent;
  }
  input:focus {
    outline: none;
  }
</style>

<div class="pin-input">
  {#if inputs.length}
    {#each inputs as item, i}
      <input
        bind:value={pins[i]}
        maxLength="1"
        id={`pin${i}`}
        type="tel"
        pattern="\d{1}"
        maxlength="1"
        on:keydown|preventDefault={event => changeHandler(event, i)}
        placeholder="" />
    {/each}
  {/if}
</div>
