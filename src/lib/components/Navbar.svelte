<script>
    import {slide} from "svelte/transition";
    import Button from "./ui/button/button.svelte";
    import Icon from '@iconify/svelte';
	import { onNavigate } from "$app/navigation";
    let open = false;

    onNavigate(()=>{
        open = false;
    })
</script>

<nav class="fixed w-full z-[1000] border-foreground/50 bg-background p-4 px-16 border-b shadow-md flex items-center gap-8">
    <button class="flex md:hidden" on:click={()=>{open=!open}}>
        <Icon icon="mdi:menu"/>
    </button>
    <h1 class="text-md font-bold">~/.</h1>
    <ul class="hidden justify-center gap-4 md:flex">
        <li>
            <a href="/"><code> home <Icon icon="mdi:home"/></code></a>
        </li>
        <li>
            <a href="/"><code> projects <Icon icon="mdi:code"/></code></a>
        </li>
        <li>
            <a href="/"><code> contact <Icon icon="mdi:contact"/></code></a>
        </li>
    </ul>
    {#if open}
    <ul transition:slide class="absolute left-0 top-0 w-screen h-screen z-[1000] flex flex-col bg-background/50 backdrop-blur-lg gap-4 md:hidden">
        <li class="p-4">
            <Button on:click={()=>{open=!open}}><Icon icon="mdi:close"/></Button>
        </li>
        <li class="p-4">
            <a href="/"><code> home <Icon icon="mdi:home"/></code></a>
        </li>
        <li class="p-4">
            <a href="/"><code> projects <Icon icon="mdi:code"/></code></a>
        </li>
        <li class="p-4">
            <a href="/"><code> contact <Icon icon="mdi:contact"/></code></a>
        </li>
        <li>
            😺
        </li>
    </ul>
    {/if}
</nav>


<style lang=postcss>
    code{
        @apply items-center flex gap-2;
    }
    code::after{
        content: '>';
    }
    ul a:hover{
        text-decoration: solid underline;
    }
</style>