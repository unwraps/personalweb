<script lang="ts">
	import Button from '$lib/components/ui/button/button.svelte';
    import Icon from '@iconify/svelte';
    import gsap from 'gsap';
	import { onMount } from 'svelte';
    let repos = [];

    // create struct for github user reposs
    onMount(() => {
        let tl1 = gsap.timeline();
        tl1.from('section img,section h1', {opacity: 0, y: 100, duration: 1, ease: 'power4.out'})
           .from('section p, section span, section a', {
               opacity: 0,
               y: 100,
               duration: 1,
               ease: 'power4.out',
               stagger: 0.2
           }, '-=0.5')
           .from(".repos",
                {
                     opacity: 0,
                     y: 100,
                     duration: 1,
                     ease: 'power4.out',
                     stagger: 0.2
                },
                '-=0.5'
           )
           ;
        
        fetch('https://api.github.com/users/unwraps/repos')
            .then(res => res.json())
            .then(data => {
                repos = data;
                console.log(repos);
            })
    });
</script>

<main>
	<section class="grid h-screen w-full items-center">
		<div class="max-w-3xl gap-4 mx-auto px-16 grid grid-flow-row w-auto md:w-[64rem] md:grid-flow-col">
			<div>
                <img src="https://avatars.githubusercontent.com/u/86614284?v=4" width="64" height="64" class="pb-4 rounded-full" alt="">
				<h1 class="text-3xl font-bold">Hi im best!</h1>
				<p>Little known fact about me</p>
                <p>- I do code</p>
                <p>that's it</p>
                <div class="flex gap-4 items-center">
                    <a href="https://github.com/unwraps"><Icon icon="mdi:github" class="size-6"/></a> <span>|</span>
                    <a href="mailto:me@phu.best"><Icon icon="mdi:email" class="size-6"/></a>
                </div>
			</div>
            <div class="flex justify-center items-center">
				<a href="https://github.com/unwraps"><Button>View my port tho</Button></a>
			</div>
		</div>
	</section>
    <section class="border-t border-foreground/50">
        <div class="mx-auto justify-center">
            <!-- <div class="flex justify-center h-96 w-full items-center">
                <Icon icon="svg-spinners:180-ring-with-bg" class="size-10"/>
            </div> -->
            <div class="grid grid-cols-1 md:grid-cols-2 p-16 gap-8">
                {#each repos as repo}
                <div class="repos border shadow-md border-foreground max-w-[32rem] max-h-[24rem] rounded-xl">
                    <div class="p-4">
                        <h1 class="text-2xl font-bold">{repo.name}</h1>
                        <p>{repo.description}</p>
                        <div class="flex gap-4 items-center">
                            <a href={repo.html_url}><Icon icon="mdi:github" class="size-6"/></a>
                            <span>|</span>
                            <span>{repo.language}</span>
                        </div>
                    </div>
                </div>
                {/each}
            </div>
        </div>
    </section>
</main>
