<script>
  import { text } from "@sveltejs/kit";
  import { nanoid } from "nanoid";

  let textInInputField = $state("");
  const { tasks, saveToStorage } = $props();
</script>

<div class="bg-slate-700/100 z-50 py-2 w-[100%] my-2 flex flex-row justify-center items-center fixed bottom-0">
  <!-- <input
    type="text"
    class="bg-slate-200 p-2 mx-3 rounded-2xl w-[80%] px-4"
    bind:value={textInInputField}
  /> -->
  <div class="group">

    <input
      id="query"
      class="input"
      type="search"
      placeholder="Add Task..."
      name="searchbar"
      bind:value={textInInputField}
    />
  </div>



  <button
    aria-label="x"
    class="group cursor-pointer outline-none hover:rotate-90 duration-300"
    onclick={() => {
      if (textInInputField == '' || textInInputField == ' ') return

      tasks.push({
        text: textInInputField,
        id: nanoid(),
        finished: false,
      });
      // alert('task added')
      textInInputField = "";
      saveToStorage()
    }}
  >
    <!-- <img
      class="w-[2.3em] h-[2.3em] hover:scale-105"
      alt="plusBtn"
      src="https://cdn-icons-png.flaticon.com/512/1828/1828817.png"
    /> -->

    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="35px"
      height="35px"
      viewBox="0 0 24 24"
      class="stroke-zinc-400 fill-none group-hover:fill-zinc-800 group-active:stroke-zinc-200 group-active:fill-zinc-600 group-active:duration-0 duration-300"
    >
      <path
        d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z"
        stroke-width="1.5"
      ></path>
      <path d="M8 12H16" stroke-width="1.5"></path>
      <path d="M12 16V8" stroke-width="1.5"></path>
    </svg>
  </button>
</div>


<style>
  .group {
    display: flex;
    line-height: 28px;
    align-items: center;
    position: relative;
    max-width: 100vw;
  }

  .input {
    font-family: "Montserrat", sans-serif;
    width: 80vw;
    height: 45px;
    padding-left: 1rem;
    box-shadow: 0 0 0 1.5px #2b2c37, 0 0 25px -17px #000;
    border: 0;
    border-radius: 12px;
    background-color: #16171d;
    outline: none;
    color: #bdbecb;
    transition: all 0.25s cubic-bezier(0.19, 1, 0.22, 1);
    cursor: text;
    z-index: 0;
    margin-right: 1em;
  }

  .input::placeholder {
    color: #bdbecb;
  }

  .input:hover {
    box-shadow: 0 0 0 2.5px #2f303d, 0px 0px 25px -15px #000;
  }

  .input:active {
    transform: scale(0.995);
  }

  .input:focus {
    box-shadow: 0 0 0 2.5px #2f303d;
  }

  .search-icon {
    position: absolute;
    left: 1rem;
    fill: #bdbecb;
    width: 1rem;
    height: 1rem;
    pointer-events: none;
    z-index: 1;
  }
</style>