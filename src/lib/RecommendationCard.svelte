<script>
	import { fade } from 'svelte/transition';
	import LoadingCard from './LoadingCard.svelte';

	export let recommendation;

	async function getRecommendationInfo() {
		const response = await fetch('/api/getMediaDetails', {
			method: 'POST',
			body: JSON.stringify({ title: recommendation.title }),
			headers: {
				'content-type': 'application/json'
			}
		});
		let recommendationDetails = await response.json();

		return recommendationDetails;
	}

	let promise = getRecommendationInfo();
</script>

<div>
	{#await promise}
		<LoadingCard incomingStream={false} />
	{:then data}
		{#if data.Poster}
			<div in:fade class="relative flex flex-col md:flex-row bg-neutral-800/70 shadow-md p-6">
				<div class="z-40 flex flex-col justify-between md:ml-6 pt-32 md:pt-0 w-full">
					<div>
						<div class="flex items-end mb-4">
							<div class="font-bold text-slate-200 text-3xl">
								{data.Title}
								<span class="font-bold text-slate-200/60 text-xl ml-2">{data.Year}</span>
							</div>
						</div>
						<div class="text-slate-200/90 mb-4">
							{data.Plot}
						</div>
						<div class="text-slate-200/50 mb-4">
							Starring: {data.Actors}
						</div>
					</div>
					<div class="flex items-center">
						<div class="mr-4 py-1 px-2 rounded-full text-pink-600 border border-pink-600 text-xs">
							{data.Rated}
						</div>
					</div>
				</div>
			</div>
		{:else}
			<div in:fade class="relative flex flex-col md:flex-row bg-neutral-800/70 shadow-md p-6">
				<div class="z-40 flex flex-col justify-between md:ml-6 w-full">
					<div>
						<div class="flex items-end mb-4">
							<div class="font-bold text-slate-200 text-3xl">
								{recommendation.title}
								<span class="font-bold text-slate-200/60 text-xl ml-2">N/A</span>
							</div>
						</div>
						<div class="text-slate-200/90 mb-4">
							{recommendation.description}
						</div>
					</div>
				</div>
			</div>
		{/if}
	{:catch error}
		<div in:fade class="relative flex flex-col md:flex-row bg-neutral-800/70 shadow-md p-6">
			<div class="z-40 flex flex-col justify-between md:ml-6 w-full">
				<div>
					<div class="flex items-end mb-4">
						<div class="font-bold text-slate-200 text-3xl">
							{recommendation.title}
							<span class="font-bold text-slate-200
