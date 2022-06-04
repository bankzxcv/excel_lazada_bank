<script>
  import { onMount } from "svelte"
  let sp
  onMount(async () => {
    const spreadsheet = await (await import("x-data-spreadsheet")).default
    sp = new spreadsheet("#spread")
  })
</script>


<div id="spread" />
