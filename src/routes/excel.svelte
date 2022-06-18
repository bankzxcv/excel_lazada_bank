<script>
  // import { onMount } from "svelte"
  // let sp
  // onMount(async () => {
  //   const spreadsheet = await (await import("x-data-spreadsheet")).default
  //   sp = new spreadsheet("#spread")
  // })
  // import xlsx from "xlsx"
  import { merge } from "../stores/mergeCell"
  import * as XLSX from "xlsx/xlsx.mjs"
  // merge.subscribe(e => {
  //   show = e
  // })
</script>

<div>
  <div>{$merge ?? 0}</div>
  <!-- <div class="w-screen h-screen" id="spread" /> -->
</div>
