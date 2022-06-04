<script>
  import "../app.css"
  import { page } from "$app/stores"
  import { beforeNavigate, goto } from "$app/navigation"
  const navs = [
    { title: "HOME", path: "/" },
    { title: "EXCEL", path: "/excel" },
  ]
  console.log($page.url.pathname)
</script>

<header class="text-gray-400 body-font">
  <nav class="flex flex-row pt-4 pr-4">
    <ul class="flex flex-row ml-auto mr-4">
      {#each navs as { title, path }}
        <li class="px-2 py-2">
          <!-- <a class:active={$page.url.pathname === path} href={path}>{title}</a> -->
          {console.log(path)}
          <a class:text-gray-1000={$page.url.pathname === path} href={path}>{title}</a>
        </li>
      {/each}
    </ul>
  </nav>
</header>
<slot />
