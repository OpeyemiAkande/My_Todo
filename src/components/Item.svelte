<script>
  import { createEventDispatcher } from "svelte";
  export let id, title, text, completed;

  const dispatch = createEventDispatcher();

  function triggerUpdate() {
    dispatch("update", { id, title, text, completed });
  }

  function handleDoubleClick() {
    const yes = confirm("Are you sure you wish to delete this item?");

    if (yes) {
      dispatch("delete", id);
    }
  }

  let hiddenDiv = document.createElement("div");
  let textarea;
  //   console.log(textarea);
  let content = null,
    startingHeight;

  hiddenDiv.classList.add("txta");
  hiddenDiv.style.display = "none";
  hiddenDiv.style.whiteSpace = "pre-wrap";
  hiddenDiv.style.overflowWrap = "anywhere";

  const handleInput = ({ key, target }) => {
    key === "Escape" && target.blur();
    // console.log(textarea);

    textarea.parentNode.appendChild(hiddenDiv);

    content = textarea.value;
    content = content.replace(/\n/g, "<br>");
    hiddenDiv.innerHTML = content + '<br style="line-height: 3px;">';

    hiddenDiv.style.visibility = "hidden";
    hiddenDiv.style.display = "block";
    textarea.style.height = hiddenDiv.offsetHeight + "px";
    // startingHeight = +(hiddenDiv.offsetHeight + "px");

    // console.log(startingHeight);
    hiddenDiv.style.visibility = "visible";
    hiddenDiv.style.display = "none";

    console.log(textarea.offsetHeight);
  };
</script>

<div class="item" class:completed on:dblclick={handleDoubleClick}>
  <div class="header">
    <input
      type="text"
      class="title-input"
      bind:value={title}
      on:keyup={({ key, target }) => key === "Enter" && target.blur()}
      on:blur={() => triggerUpdate()}
      placeholder="Title"
    />
    <input
      type="checkbox"
      class="completed-checkbox"
      bind:checked={completed}
      on:change={() => triggerUpdate()}
    />
  </div>
  <textarea
    type="text"
    class="text-input"
    bind:this={textarea}
    bind:value={text}
    readonly={completed}
    on:keyup={handleInput}
    on:blur={() => triggerUpdate()}
  />
</div>

<style>
  .item {
    display: flex;
    flex-direction: column;
    padding: 15px;
    background: #fff;
    border-radius: 9px;
    width: 240px;

    /* overflow-y: scroll; */
  }

  .item {
    margin-bottom: 24px;
    margin-right: 20px;
  }

  .item.completed {
    background: #ddd;
  }

  .item.completed .text-input {
    color: #555;
    text-decoration: line-through;
  }

  .item:focus-within {
    background: rgba(255, 255, 255, 0.8);
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .title-input {
    background: none;
    border: none;
    outline: none;
    font-weight: 700;
    font-size: 1em;
  }

  .title-input::placeholder {
    color: #777;
    font-weight: 700;
  }

  .text-input::-webkit-scrollbar {
    display: none;
  }

  .text-input {
    /* flex-grow: 1; */
    background: none;
    border: none;
    outline: none;
    font-weight: 500;
    font-size: 1em;
    margin-bottom: 0;

    /* min-height: 100px; */
    overflow: hidden;
    height: auto;
    resize: none;
  }

  .completed-checkbox {
    /* margin-left: 15px; */
    margin-bottom: 0;
  }
</style>
