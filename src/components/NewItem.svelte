<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  let value = "";

  function handleKeyUp({ key }) {
    if (key !== "Enter" || value.length === 0) return;
    dispatch("newitem", value);
    value = "";
  }
</script>

<input type="text" on:keyup={handleKeyUp} bind:value placeholder="+ Add Item" />

<style>
  input {
    box-sizing: border-box;
    margin-bottom: 15px;
    padding: 15px;
    border: none;
    outline: none;
    width: 100%;
    background: rgba(0, 0, 0, 0.75);
    color: #fff;
    font-weight: bold;
    font-size: 1em;
    cursor: pointer;
    border-radius: 9px;
  }

  input::placeholder {
    color: #fff;
  }
</style>
