<script>
  import { onMount } from "svelte"
  let sp
  onMount(async () => {
    const spreadsheet = await (await import("x-data-spreadsheet")).default
    sp = new spreadsheet("#x-demo")
  })
  let a
  let b
  $: {
    if (a) {
      console.log("---a---")
      console.log(a)
    }
    if (b) {
      console.log("---b--")
      console.log(b)
    }
  }
</script>

<header class="text-gray-600 body-font">
  <div class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center">
    <nav class="md:ml-auto flex flex-wrap items-center text-base justify-center">
      <h1>Lazada Summary</h1>
    </nav>
  </div>
</header>

<div class="mt-6 flex flex-col divide-y items-center justify-center">
  <div class="my-6 flex flex-col items-center justify-center min-w-[75%] border">
    <div class="mt-4" />
    <div class="flex flex-row items-center justify-center">
      <strong class="block text-gray-700 text-sm font-bold mb-2 mt-2">File A</strong>
      <input class="mx-4 border hover:bg-gray-200" type="file" bind:files={a} />
    </div>
    <div class="flex flex-row items-center justify-center">
      <strong class="block text-gray-700 text-sm font-bold mb-2 mt-2">File B</strong>
      <input class="mx-4 border hover:bg-gray-200" type="file" bind:files={b} />
    </div>

    <div>
      <button
        class="btn btn-primary border-2 bg-gray-200 border-gray-500 bg-rounded-md mt-4 mb-4 hover:bg-gray-400 px-4"
        on:click={e => {
          console.log(e)
        }}>CLEAR Files</button
      >
    </div>
  </div>
  ------------
  <div id="x-demo" />
</div>
