<script>
  import { scale, fly } from 'svelte/transition';
  import { BaseTransition } from "@sveltech/routify/decorators"

  export let scoped
  const { width } = scoped

  const transitionConfigs = [
    {
      // New and old route are identical, do nothing
      condition: ({ routes }) => routes[0] === routes[1],
      transition: () => {},
    },
    {
      condition: c => c.toAncestor,
      transition: scale,
      inParams: { start: 1.2 },
      outParams: { start: 0.8 },
    },
    {
      condition: c => c.toDescendant,
      transition: scale,
      inParams: { start: 0.8 },
      outParams: { start: 1.2 },
    },
    {
      condition: c => c.toHigherIndex,
      transition: fly,
      inParams: { x: $width, duration: 500 },
      outParams: { x: -$width, duration: 500 },
    },
    {
      condition: c => c.toLowerIndex,
      transition: fly,
      inParams: { x: -$width, duration: 500 },
      outParams: { x: $width, duration: 500 },
    },
    {
      // No matching config. We don't want a transition
      condition: () => true,
      transition: fly,
      inParams: { x: -$width, duration: 500 },
      outParams: { x: $width, duration: 500 },
    }
  ]
</script>

<BaseTransition configs={transitionConfigs}>
  <slot />
</BaseTransition>
