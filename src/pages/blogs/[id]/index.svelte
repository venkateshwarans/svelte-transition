<script>
import { params } from "@sveltech/routify";

  export let scoped;
  $: blog = scoped.show;
</script>





{#if blog}
<article>
  <img
    src={blog.image.medium}
    alt="cover"
    style="float: left; margin-right: 2em;" />
  <h1>{blog.name}</h1>
  <p>
    {@html blog.summary}
  </p>
</article>
{/if}



<!-- <pre>{JSON.stringify(blog)}
</pre> -->
<!-- <a href={$url('/blogs')}>Back</a> -->
