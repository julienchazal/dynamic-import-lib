<script lang="ts">
	import lottie, { type AnimationItem } from 'lottie-web';
	import { onMount, tick } from 'svelte';

	export let name: string;

	let icon: AnimationItem;
	let container: HTMLElement;


	const initLottie = async () => {
		const data = (await import(`../lottie/${name}.json`)).default;

		if (icon) {
			icon.destroy();
		}

		if (data) {
			icon = lottie.loadAnimation({
				container: container,
				animationData: data,
				loop: false,
				autoplay: false
			});
		}

		icon.goToAndPlay(`hover-${name}`);
	};

	onMount(async () => {
		// garantit que le DOM est complètement mis à jour
		await tick();
		if (name) {
			await initLottie();
		}
	});
</script>

<div
	bind:this={container}
	role="img"
	aria-label="pictogramme"
/>

<style lang="postcss">
    div {
				position: relative;
        width: 30px;
        height: 30px;
    }
		div :global(svg) {
				stroke: currentColor;
		}
</style>
