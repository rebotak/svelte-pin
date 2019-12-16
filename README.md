## Masked PIN input components for svelte.

### Install:

```sh
npm i -s svelte-pin
```

### Usage:

```js
<script>
  import PinInput from 'svelte-pin';
  let value;
</script>

<PinInput size={6} bind:pin={value} />
<h1>PIN: {value}</h1>

```

### Props:

| Prop | Default value | Description                                              |
| ---- | ------------- | -------------------------------------------------------- |
| pin  | ''            | Value of the input. need to bind to component's variable |
| size | 6             | Length of the pin input                                  |

### Run examples at local
