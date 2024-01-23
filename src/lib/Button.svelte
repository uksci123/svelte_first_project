<script>
  // @ts-nocheck
  let isLeftHovered;
</script>

<button
  class="py-4 pr-12 m-8 bg-red-500 rounded-lg text-white font-semibold text-lg active:translate-y-1.5 flex"
  class:disable={isLeftHovered}
  class:pl-12={!$$slots.leftContent}
>
  {#if $$slots.leftContent}
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    <div
      class="px-4 flex"
      on:mouseenter={() => (isLeftHovered = true)}
      on:mouseleave={() => (isLeftHovered = false)}
    >
      <slot {isLeftHovered} name="leftContent" />
    </div>
  {/if}
    <slot>fallback</slot>
</button>
