<svelte:options tag="flx-button" />

<script lang="ts">
  import { onMount, createEventDispatcher } from 'svelte'
  import { get_current_component } from 'svelte/internal'

  const component = get_current_component()
  const svelteDispatch = createEventDispatcher()

  const dispatch = (name, detail) => {
    svelteDispatch(name, detail)
    component?.dispatchEvent(new CustomEvent(name, { detail }))
  }

  let className = ''
  export let label = ''
  export { className as class }
  export let style = ''

  export let objectInput = {}

  onMount(() => {
    console.log('onMount', objectInput)
    setTimeout(() => {
      console.log('after some time', objectInput)
    })
  })

  function sayHello() {
    dispatch('message', {
      text: 'Hello!',
    })
  }
</script>

<button class={`btn-indigo ${className}`} {style} on:click={sayHello} part="button">
  {label}
</button>

<style lang="postcss">
  @tailwind base;

  .btn-indigo {
    @apply py-2 px-4 bg-indigo-500 text-white font-semibold rounded-lg shadow-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-400 focus:ring-opacity-75;
  }
</style>
