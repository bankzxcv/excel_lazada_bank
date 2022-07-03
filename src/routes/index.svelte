<script>
  import * as XLSX from "xlsx/xlsx.mjs"
  import papa from "papaparse"
  import { merge } from "../stores/mergeCell"

  let a
  let b
  let counting = 1
  const indexer = {}
  const column = {}

  const doa = () => {
    const rows = a
    for (let i = 0; i < rows.length; i++) {
      const row = rows[i]
      const txTxt = "หมายเลขการสั่งซื้อ"
      const txId = row[txTxt]
      if (txId && typeof indexer[txId.trim()] !== "number") {
        indexer[txId.trim()] = i
      }
    }
  }
  const dob = () => {
    const rows = b

    const indFeeName = 2
    const indAmount = 7
    const indOrderNumber = 13
    const rowA = a
    for (let i = 0; i < rows.length; i++) {
      const data = rows[i]
      const feeName = data[indFeeName]
      const amount = data[indAmount]
      const orderNumber = data[indOrderNumber].trim()
      if (typeof indexer[orderNumber] === "number") {
        const idx = indexer[orderNumber]
        a[idx][feeName] = amount
      }
    }

    for (let i = 0; i < a.length; i++) {
      const row = a[i]
      const keys = Object.keys(row)
      for (let j = 0; j < keys.length; j++) {
        const key = keys[j]
        column[key] = ""
      }
    }

    console.log(column)
    const csv = papa.unparse([column, ...a])
    // console.log(csv)
    // export
    var csvData = new Blob([csv], { type: "text/csv;charset=utf-8;" })
    var csvURL = null
    if (navigator.msSaveBlob) {
      csvURL = navigator.msSaveBlob(csvData, "download.csv")
    } else {
      csvURL = window.URL.createObjectURL(csvData)
    }
    var tempLink = document.createElement("a")
    tempLink.href = csvURL
    tempLink.setAttribute("download", "download.csv")
    tempLink.click()
  }
  const parsing = (file, finalFile) =>
    papa.parse(file, {
      header: finalFile === "a",
      complete: ({ data }) => {
        if (finalFile === "a") {
          a = data
          doa()
        } else {
          b = data
          dob()
        }
        // merge.update(e => (e ? e++ : couting))
      },
    })
  const changeA = e => {
    const [file] = e.target.files
    if (file) {
      parsing(file, "a")
    }
  }
  const changeB = e => {
    const [file] = e.target.files
    if (file) {
      parsing(file, "b")
    }
  }
  const clearButton = () => {
    document.getElementById("inputA").value = ""
    a = null
    document.getElementById("inputB").value = ""
    b = null
  }

  const downloadButton = () => {
    merge.update(e => {
      return e ? ++e : couting
    })
    // clearButton()
  }

  $: () => {
    // if a & b reader
  }
</script>

<div class="mt-6 flex flex-col divide-y items-center justify-center">
  <div class="my-6 flex flex-col items-center justify-center min-w-[75%] border">
    <div class="mt-4" />
    <div class="flex flex-row items-center justify-center">
      <strong class="block text-gray-700 text-sm font-bold mb-2 mt-2 px-4">File A</strong>
      <input
        id="inputA"
        class="block text-sm text-slate-500 w-full
        file:mr-4 file:py-2 file:px-4
        file:rounded-full file:border-0
        file:text-sm file:font-semibold
        file:bg-violet-50 file:text-violet-700
        hover:file:bg-violet-100"
        type="file"
        on:change={changeA}
      />
      <strong> {a ? a.length : 0} rows</strong>
    </div>
    <div class="flex flex-row items-center justify-center">
      <strong class="block text-gray-700 text-sm font-bold mb-2 mt-2 px-4">File B</strong>
      <input
        id="inputB"
        class="block text-sm text-slate-500 w-full
        file:mr-4 file:py-2 file:px-4
        file:rounded-full file:border-0
        file:text-sm file:font-semibold
        file:bg-violet-50 file:text-violet-700
        hover:file:bg-violet-100"
        type="file"
        on:change={changeB}
      />
      <strong> {b ? b.length : 0} rows</strong>
    </div>

    <div>
      <button
        class="btn btn-primary border-1 bg-gray-200 border-gray-400 bg-rounded-md mt-4 mb-4 hover:bg-gray-400 px-4 rounded-lg font-light"
        on:click={downloadButton}>DOWNLOAD</button
      >
      <button
        class="btn btn-primary border-1 bg-gray-200 border-gray-400 bg-rounded-md mt-4 mb-4 hover:bg-gray-400 px-4 rounded-lg font-light"
        on:click={clearButton}>CLEAR Files</button
      >
      <button
        class="btn btn-primary border-1 bg-gray-200 border-gray-400 bg-rounded-md mt-4 mb-4 hover:bg-gray-400 px-4 rounded-lg font-light"
        on:click={() => {}}>TEST</button
      >
    </div>
  </div>
</div>
