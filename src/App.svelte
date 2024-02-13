<script>
  import Counter from "./lib/Counter.svelte";

  let items = [{ name: "new", number: 0 }];

  /**
   * @param {number} index
   */
  function increment(index) {
    items[index].number += 1;
  }
  
  /**
   * @param {number} index
   */
  function decrement(index) {
    if (items[index].number > 0) {
      items[index].number -= 1;
    }
  }

  /**
   * @param {number} index
   * @param {string} text
   */
  function changeTitle(index, text) {
    items[index].name = text;
  }

  function addCounter() {
    items = [...items, { name: "new", number: 0 }];
  }

  /**
   * @param {number} index
   */
  function removeCounter(index) {
    items = items.filter((_, id) => id !== index);
  }
</script>

<div class="text-center">
  <h1 class="text-[4rem]">Multiple Counter</h1>
  {#each items as { name, number }, index (index)}
    <Counter
      {name}
      {number}
      on:remove={() => removeCounter(index)}
      on:increment={() => increment(index)}
      on:decrement={() => decrement(index)}
      on:changeTitle={(e) => changeTitle(index, e.detail.text)}
    />
  {/each}
  <button
    class="
      max-w-sm 
      w-full 
      rounded 
      text-white 
      cursor-pointer 
      text-center 
      bg-[#68d391]
    "
    on:click={addCounter}
  >
    new counter
  </button>
  <p>title list: {items.map((counter) => counter.name).join(", ")}</p>
  <p>sum of count: {items.reduce((total, { number }) => total + number, 0)}</p>
</div>
