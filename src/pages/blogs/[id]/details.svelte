<script>
export let scoped;
$: show = scoped.show;
const keys = ["language", "runtime", "status", 'url', 'officialSite'];
</script>


{#each keys as key}
  {key} - {show[key]}
{/each}
