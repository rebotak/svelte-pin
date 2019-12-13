## Masked PIN input components for svelte.

### Run demo at local:

```
git clone git@github.com:xnimorz/svelte-input-mask.git
cd svelte-input-mask/demo
npm install
npm run dev
```

### Install:

```sh
npm install --save svelte-input-mask
```

or yarn:

```sh
yarn add svelte-input-mask
```

### Usage:

```js
<script>
  import PinInput from 'svelte-pin-input';
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
