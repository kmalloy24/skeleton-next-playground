<script lang="ts">
	import GridGallery from '$lib/components/GridGallery.svelte';
	import QuadGallery from '$lib/components/QuadGallery.svelte';
	import MasonryGallery from '$lib/components/MasonryGallery.svelte';
	import FeaturedGallery from '$lib/components/FeaturedGallery.svelte';

	import { Tabs } from '@skeletonlabs/skeleton-svelte';

	let group = $state('grid');
	let loading = $state(false);

	function handleTabChange() {
		loading = true;
		// Simulate loading time
		setTimeout(() => {
			loading = false;
		}, 1000); // Adjust this time as needed
	}
</script>

<div class="m-8">
	<div class="my-4 flex items-center justify-between">
		<h1 class="h1 text-primary-500">Skeleton NEXT Image Layouts</h1>
		<a
			href="https://github.com/kmalloy24/skeleton-next-playground"
			target="_blank"
			class="btn preset-filled-secondary-500"
		>
			<span>Code</span>
			<span>&rarr;</span>
		</a>
	</div>

	<Tabs>
		{#snippet list()}
			<Tabs.Control bind:group name="grid" on:click={handleTabChange}>Grid</Tabs.Control>
			<Tabs.Control bind:group name="quad" on:click={handleTabChange}>Quad</Tabs.Control>
			<Tabs.Control bind:group name="masonry" on:click={handleTabChange}>Masonry</Tabs.Control>
			<Tabs.Control bind:group name="feat" on:click={handleTabChange}>Featured</Tabs.Control>
		{/snippet}
		{#snippet panels()}
			{#if loading}
				<div class="flex h-64 items-center justify-center">
					<figure
						class="aspect-square size-10 animate-spin rounded-full bg-gradient-conic from-transparent to-primary-500"
					></figure>
				</div>
			{:else}
				<div class="m-12">
					<Tabs.Panel bind:group value="grid">
						<!-- <GridGallery /> -->
					</Tabs.Panel>
					<Tabs.Panel bind:group value="quad">
						<!-- <QuadGallery /> -->
					</Tabs.Panel>
					<Tabs.Panel bind:group value="masonry">
						<!-- <MasonryGallery /> -->
					</Tabs.Panel>
					<Tabs.Panel bind:group value="feat">
						<!-- <FeaturedGallery /> -->
					</Tabs.Panel>
				</div>
			{/if}
		{/snippet}
	</Tabs>
</div>
