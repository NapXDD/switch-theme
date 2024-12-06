<script lang="ts">
	import { onMount } from "svelte";
    let isDark = $state(false)
    const switchTheme = () => {
        if(isDark){
            document.documentElement.setAttribute('data-theme', 'light')
        } else {
            document.documentElement.setAttribute('data-theme', 'dark')
        }
        isDark = !isDark
    }

    onMount(() => {
        const prefersDarkMode = window.matchMedia('(prefers-color-scheme: dark)')
        if(prefersDarkMode.matches){
            isDark = true
        }
    })
</script>

<button class="bg-white text-black" onclick={switchTheme}>switch theme</button>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>


