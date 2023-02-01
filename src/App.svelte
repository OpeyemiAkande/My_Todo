<script>
  import Header from "./components/Header.svelte";
  import List from "./components/List.svelte";
</script>

<div class="container">
  <Header />
  <List />
</div>

<style>
  .container {
    width: 1200px;
    background: #ddd;
    margin: 100px auto;
    border-radius: 12px;
  }

  :global(.container *) {
    font-family: sans-serif;
  }
</style>
