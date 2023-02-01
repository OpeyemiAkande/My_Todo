<script>
  import { items } from "../stores";

  $: itemCount = $items.length;
  $: completedItemCount = $items.filter((item) => item.completed).length;
</script>

<div class="header">
  <span>Todo List</span>
  <span>{completedItemCount}/{itemCount}</span>
</div>

<style>
  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
    color: #ffffff;
    font-weight: bold;
    font-size: 1.5rem;
    background: rgba(0, 0, 0);
    border-top-left-radius: 12px;
    border-top-right-radius: 12px;
  }
</style>
