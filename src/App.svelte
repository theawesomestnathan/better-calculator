<script lang="ts">
  import { evaluate } from "mathjs";

  const buttons: string[] = [
    "C",
    ".",
    "%",
    "/",
    "7",
    "8",
    "9",
    "+",
    "4",
    "5",
    "6",
    "-",
    "1",
    "2",
    "3",
    "*",
    "(",
    "0",
    ")",
    "="
  ];
  let equation: string = "";

  function btnPressed(digit: string) {
    const ordinaryButtons: string = "0123456789+-*/%.()";

    if (ordinaryButtons.includes(digit)) {
      if (equation === undefined) {
        equation = "";
      }
      equation += digit;
    }
    else if (digit === "C") equation = "";
    else if (digit === "=") {
      try {
        equation = evaluate(equation);
      }
      catch (error) {
        console.error("Error: " + error);
      }
    }
  }
</script>

<main class="bg-gradient-to-r from-slate-800 to-white h-screen text-white">
  <div class="flex justify-center pt-52">
    <div class="bg-black/25 w-96 rounded p-3">
      <h1 class="text-3xl pb-3"> calculator </h1>

      <input 
        class="bg-transparent border-none outline-none text-2xl"  
        bind:value={equation}
        readonly/>

      <div class="pt-5 grid grid-cols-4 gap-2">
        {#each buttons as button} 
          <button 
            class="bg-gray-400 w-14 h-14 rounded" 
            on:click={() => btnPressed(button)}> {button} </button>
        {/each}
      </div>
    </div>
  </div>
</main>