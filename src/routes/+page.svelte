<script>
    import init, { greet, crunch, goodbye } from "wasm";
    // we need onMount to run init
    import { onMount } from "svelte";
  
    onMount(async () => {
      await init(); // init initializes memory addresses needed by WASM and that will be used by JS/TS
    })

    /**
	 * @param {number} num
	 */
    function fib_ts(num) {
        if (num <= 2) {
            return 1;
        }
        let next = 0;
        let curr = 1;
        let prev = 1;
        for (let i = 0; i < num-2; i++) {
            next = curr + prev;
            prev = curr;
            curr = next;
            console.log(curr);
        }
        return curr;
    }

    let x = 4;
  </script>
  
  <div>
    <h1>Test Redeployment</h1>
    <button on:click={() => {greet("Pirro")}}>Click Me</button>
    <button on:click={() => {x = crunch(new Uint8Array([1,2, 3, 4]))}}>{x}</button>
    <button on:click={() => {goodbye()}}>goodbye</button>
    <button on:click={() => {x = fib_ts(200)} }>fib js</button>
  </div>
  