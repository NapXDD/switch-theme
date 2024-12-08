<script lang="ts">
	import { page } from "$app/stores";
	import { onMount } from "svelte";
	import { derived, get } from "svelte/store";
    let isDark = $state(false)
    let theme = ['light', 'dark']

    const switchTheme = () => {
        if(!isDark){
            document.documentElement.setAttribute('data-theme', 'light')
        } else {
            document.documentElement.setAttribute('data-theme', 'dark')
        }
    }

    onMount(() => {
        const prefersDarkMode = window.matchMedia('(prefers-color-scheme: dark)')

        if(prefersDarkMode.matches){
            isDark = true
        }

        window.matchMedia('(prefers-color-scheme: dark)')
            .addEventListener('change',({ matches }) => {
        if (matches) {
            isDark = true
        } else {
            isDark = false
        }
        switchTheme()
        })
    })

    const toggleTheme = () => {
        isDark = !isDark
        switchTheme()
    }

    $effect(() => {
        const paramArr = Array.from($page.url.searchParams.entries())[0]
        if(!paramArr) return
        const paramKey = paramArr[0]
        const paramValue = paramArr[1]
        if(paramKey !== 'theme'){
            return
        }
        if(!theme.includes(paramValue)){
            document.documentElement.setAttribute('data-theme', '')
        }
        if(paramValue === 'dark'){
            isDark = true
        } else if(paramValue === 'light'){
            isDark = false
        }
        switchTheme()
    })
</script>

<button class="bg-white text-black" onclick={toggleTheme}>switch theme</button>
<br/>
<a href="?theme=light">change to light theme</a>
<br/>
<a href="?theme=dark">change to dark theme</a>
<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>


