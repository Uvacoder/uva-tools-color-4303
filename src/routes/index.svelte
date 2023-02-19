<script lang="ts">
  export const ssr = false
  import { Color } from '$src/models/Color'

  import { primaryColor } from '$src/store'
  import { copyToClipboard } from '$src/utils/clipboard'

  $primaryColor = Color.random()

  const tools = ['mix', 'info', 'blend', 'modify']

  const handleMouseEnter = (e) => {
    $primaryColor = Color.random()
  }

  $: colorHex = $primaryColor.toString('hex')
</script>

<svelte:head>
  <title>tools4color</title>
</svelte:head>


  <div class="text-center">
    <h1
      class="text-5xl sm:text-7xl md:text-8xl font-bold mb-3 text-primary-clamped transition"
    >
      tools4color
    </h1>
    <p class="text-base sm:text-xl dark:text-gray-400 text-gray-500">
      An <a
        href="https://github.com/uvacoder/uva-tools-color-4303"
        class="dark:text-gray-300 text-gray-800 hover:text-primary-clamped transition"
        target="_blank">open source</a
      > toolbox for colors.
    </p>
  </div>

  <div
    class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 mt-8 sm:mt-14 gap-3 sm:gap-5"
  >
    {#each tools as tool}
      <a
        href={'/' + tool}
        class="transition transform hover:-translate-y-1 bg-white dark:bg-transparent border dark:border-gray-700/60 border-gray-300 shadow dark:shadow-black/50 rounded-lg hover:!bg-primary hover:!text-primary-text hover:!border-primary hover:shadow-xl dark:hover:shadow-black/30 uppercase px-8 py-4 text-center"
        on:mouseenter={handleMouseEnter}
      >
        <span class="font-semibold text-base sm:text-lg tracking-widest"
          >{tool}</span
        >
      </a>
    {/each}
  </div>

  {#key colorHex}
    <div
      on:click={(e) => copyToClipboard(e, colorHex)}
      class="absolute bottom-0 left-1/2 transform -translate-x-1/2 text-primary-clamped font-medium tracking-wide font-mono cursor-pointer text-sm"
    >
      {colorHex}
    </div>
  {/key}
</div>
