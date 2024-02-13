<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let number: number = 0;
  export let name: string = "new";

  const reset = () => {
    dispatch("reset");
  };

  const remove = () => {
    dispatch("remove");
  };

  const increment = () => {
    dispatch("increment");
  };

  const decrement = () => {
    dispatch("decrement");
  };

  const changeTitle = (event: Event) => {
    const target = event.target as HTMLInputElement;
    dispatch("changeTitle", {
      text: target.value,
    });
  };
</script>

<div
  class="
    relative
    flex 
    items-center 
    m-auto 
    max-w-sm 
    bg-[#f7fafc] 
    rounded 
    shadow-lg 
    mb-2"
>
  <input
    class="w-32 px-1 text-[#718096] mx-4"
    value={name}
    on:input={changeTitle}
  />
  <span class="text-center font-bold text-lg ml-[10px] px-4">{number}</span>
  <div class="flex justify-center items-center ml-auto my-1">
    <button
      class="py-1 px-3 text-[18px] bg-red-500 rounded-l text-white"
      on:click={increment}
    >
      +
    </button>
    <button
      class="py-1 px-3 text-[18px] bg-blue-500 text-white"
      on:click={decrement}
    >
      -
    </button>
    <button
      class="py-1 px-3 text-[18px] bg-yellow-500 rounded-r text-white"
      on:click={reset}
    >
      0
    </button>
    <button
      class="px-4 text-[#a0aec0]" 
      on:click={remove}
    >
      x
    </button>
  </div>
</div>
