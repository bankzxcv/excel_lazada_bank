<script>
  import "../app.css"
  import { page } from "$app/stores"
  // import { beforeNavigate, goto } from "$app/navigation"
  const navs = [
    { title: "HOME", path: "/" },
    { title: "EXCEL", path: "/excel" },
  ]
  console.log($page.url.pathname)
</script>

<header class="text-gray-400 body-font">
  <nav class="flex flex-row pt-4 pr-4 border-gray-200 bg-white px-8">
    <h1 class="w-full text-black text-3xl font-bold">Excel App</h1>
    <ul class="flex flex-row ml-auto mr-4">
      {#each navs as { title, path }}
        <li class="px-2 py-2 hover:text-gray-500">
          <a class={$page.url.pathname === path ? "text-black" : ""} href={path}>{title}</a>
        </li>
      {/each}
    </ul>
  </nav>
</header>
<slot />
