<script>
  import { url, isActive } from "@sveltech/routify";
  import { writable } from 'svelte/store';
  import CustomTransition  from '../_config/CustomTransition.svelte';

  const links = [["/projects", "Projects"], ["/contact", "Contact"], ["/blogs/", "Blogs"]];

  const width = writable();

  $: urls = links.map(([path, name]) => ({
    name,
    href : $url(path),
    active: !!$isActive(path)
  }))

  $: urlOrder = urls.map(({href}) => href)

</script>

<style>
  .active {
    border-bottom: 3px solid var(--color-secondary);
  }
</style>

<header>
  <nav>
    <h1>
      <a href="/">V</a>
    </h1>
      <ul>
        {#each links as [path, name]}
          <li>
            <a href={$url(path)} class:active={$isActive(path)}>{name}</a>
          </li>
        {/each}
      </ul>
  </nav>
</header>

<main bind:offsetWidth={$width}>
  <slot decorator={CustomTransition}  scoped={{ width}}  />
</main>
