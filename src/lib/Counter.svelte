<script>
  let count = 0;
  const increment = () => {
    count += 1;
  }
  const decrement = () => {
    if (count > 0) {
      count -= 1;
    }
  }
  const updateCount = (event) => {
    const value = event.target.value;
    count = value;
  };
</script>

<style>
  input {
    text-align: center;
    font-size: 1.2em;
    margin: 0;
    padding: 0;
    width: 40px;
    height: 40px;
    border-radius: 8px;
    border: 1px solid transparent;
  }
  button {
    text-align: center;
    font-size: 1.2em;
    margin: 0;
    padding: 0;
    width: 40px;
    height: 40px;
    border-radius: 8px;
    border: 1px solid transparent;
  }
</style>

<button on:click={decrement}>
  -
</button>
<input type="text" bind:value={count} on:input={updateCount}>
<button on:click={increment}>
  +
</button>
