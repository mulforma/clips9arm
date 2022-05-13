<script lang="ts">
  import { darkTheme } from '$lib/store';
  import Kofi from '$lib/components/Kofi.svelte';
  import SocialButtons from '$lib/components/SocialButtons.svelte';
  import '../tailwind.css';
  import '../index.css';
  import Head from '$lib/components/Head.svelte';
</script>

<button class="absolute left-2 top-2 text-lg" on:click={() => ($darkTheme = !$darkTheme)}>
  {$darkTheme ? '🌙' : '🌞'}
</button>
<div class={$darkTheme ? 'dark' : ''}>
  <Head />
  <slot />
  <Kofi name={'tinarskii'} />
  <SocialButtons />
</div>
