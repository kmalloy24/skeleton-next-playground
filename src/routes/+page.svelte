<script lang="ts">
	import GridGallery from '$lib/components/GridGallery.svelte';
	import QuadGallery from '$lib/components/QuadGallery.svelte';
	import MasonryGallery from '$lib/components/MasonryGallery.svelte';

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
		<a href="##" class="btn preset-filled-secondary-500">
			<span>Code</span>
			<span>&rarr;</span>
		</a>
	</div>

	<Tabs>
		{#snippet list()}
			<Tabs.Control bind:group name="grid" on:click={handleTabChange}>Grid</Tabs.Control>
			<Tabs.Control bind:group name="quad" on:click={handleTabChange}>Quad</Tabs.Control>
			<Tabs.Control bind:group name="masonry" on:click={handleTabChange}>Masonry</Tabs.Control>
		{/snippet}
		{#snippet panels()}
			{#if loading}
				<div class="flex h-64 items-center justify-center">
					<figure
						class="bg-gradient-conic to-primary-500 aspect-square size-10 animate-spin rounded-full from-transparent"
					></figure>
				</div>
			{:else}
				<Tabs.Panel bind:group value="grid">
					<div class="m-12">
						<GridGallery />
					</div>
				</Tabs.Panel>
				<Tabs.Panel bind:group value="quad">
					<div class="m-12">
						<QuadGallery />
					</div>
				</Tabs.Panel>
				<Tabs.Panel bind:group value="masonry">
					<div class="m-12">
						<MasonryGallery />
					</div>
				</Tabs.Panel>
			{/if}
		{/snippet}
	</Tabs>
</div>
