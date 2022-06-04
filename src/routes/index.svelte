<script>
  import papa from "papaparse"
  let a
  let b
  const parsing = (file, target) =>
    papa.parse(file, {
      config: {
        header: true,
        delimiter: "",
        newline: "",
      },
      complete: ({ data }) => {
        target = data
        console.log(data)
      },
    })
  const changeA = e => {
    const [file] = e.target.files
    if (file) {
      parsing(file, a)
    }
  }
  const changeB = e => {
    const [file] = e.target.files
    if (file) {
      parsing(file, b)
    }
  }

  const clearButton = () => {}
</script>

<div class="mt-6 flex flex-col divide-y items-center justify-center">
  <div class="my-6 flex flex-col items-center justify-center min-w-[75%] border">
    <div class="mt-4" />
    <div class="flex flex-row items-center justify-center">
      <strong class="block text-gray-700 text-sm font-bold mb-2 mt-2 px-4">File A</strong>
      <input
        class="block text-sm text-slate-500 w-full
        file:mr-4 file:py-2 file:px-4
        file:rounded-full file:border-0
        file:text-sm file:font-semibold
        file:bg-violet-50 file:text-violet-700
        hover:file:bg-violet-100"
        type="file"
        on:change={changeA}
      />
    </div>
    <div class="flex flex-row items-center justify-center">
      <strong class="block text-gray-700 text-sm font-bold mb-2 mt-2 px-4">File B</strong>
      <input
        class="block text-sm text-slate-500 w-full
        file:mr-4 file:py-2 file:px-4
        file:rounded-full file:border-0
        file:text-sm file:font-semibold
        file:bg-violet-50 file:text-violet-700
        hover:file:bg-violet-100"
        type="file"
        on:change={changeB}
      />
    </div>

    <div>
      <button
        class="btn btn-primary border-2 bg-gray-200 border-gray-500 bg-rounded-md mt-4 mb-4 hover:bg-gray-400 px-4 rounded-full"
        on:click={e => {
          console.log(e)
          clearButton()
        }}>CLEAR Files</button
      >
    </div>
  </div>
</div>
