<script>

  import BellIcon from './icons/BellIcon.svelte';
  import DbIcon from './icons/DbIcon.svelte';

  export let icon; // Prop for the SVG
  export let label = 'View notifications'; // Prop for the label text
  export let hoverColor = 'red'; // Prop for hover color (red or grey)

  // Determine the hover color class based on the prop
  $: hoverClass = hoverColor === 'red' ? 'hover:text-red-500' : 'hover:text-gray-500';

  const iconMap = {
    bell: BellIcon,
    db: DbIcon,
  };

</script>

<button type="button" class="-m-2.5 p-2.5 text-gray-400 {hoverClass}">
  <span class="sr-only">{label}</span>
  {#if typeof icon === 'string' && icon in iconMap}
    <!-- Render SVG component based on string -->
    <svelte:component this={iconMap[icon]} class="size-6" />
  {:else if icon}
    <!-- Render SVG component directly -->
    <svelte:component this={icon} class="size-6" />
  {/if}
</button>
