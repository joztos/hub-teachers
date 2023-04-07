<script>
	import LoadingIndicator from './Loading.svelte';

	/**
	 * @type string
	 */
	export let GradeLevel;
	/**
	 * @type string
	 */
	export let specificDescriptors;
	/**
	 * @type Boolean
	 */
	export let loading;

	let GradeLevels = [
		{ value: '1st grade', title: '1st grade' },
		{ value: '2nd grade', title: '2nd grade' },
		{ value: '3rd grade', title: '3rd grade' },
		{ value: '4th grade', title: '4th grade' },
		{ value: '5th grade', title: '5th grade' },
		{ value: '6th grade', title: '6th grade' },
		{ value: '7th grade', title: '7th grade' },
		{ value: '8th grade', title: '8th grade' },
		{ value: '9th grade', title: '9th grade' },
		{ value: '10th grade', title: '10th grade' },
		{ value: '11th grade', title: '11th grade' },
		{ value: '12th grade', title: '12th grade' }
	];

</script>

<div class="pt-6 md:pt-10 text-slate-200">
	<div>
		<div class="mb-8">
			<div class="mb-4 font-semibold text-lg">Select your student School level</div>
			<div class="flex items-center">
				{#each GradeLevels as type (type.value)}
					<button
						on:click={() => {
							GradeLevel = type.value;
						}}
						class={`${
							GradeLevel === type.value ? 'bg-pink-600/40' : ''
						} text-slate-200 font-bold mr-2 text-sm mt-2 py-2 px-4 rounded-full border border-pink-600`}
					>
						{type.title}
					</button>
				{/each}
			</div>
		</div>
		<div class="mt-8">
			<div class="mb-4 font-semibold text-lg">
				Choose a topic of your choice to generate the lesson plan.
			</div>
			<textarea
				bind:value={specificDescriptors}
				class="bg-white/40 border border-white/0 p-2 rounded-md placeholder:text-slate-800 text-slate-900 w-full h-20 font-medium"
				placeholder="Por ejemplo, El capitalismo en el siglo XXI."
			/>
			<button
				on:click
				class={`${
					loading
						? 'bg-pink-400/50'
						: 'bg-pink-600 hover:bg-gradient-to-r from-pink-700 via-pink-600 to-pink-700 '
				} mt-4 w-full h-10 text-white font-bold p-3 rounded-full flex items-center justify-center`}
			>
				{#if loading}
					<LoadingIndicator />
				{:else}
					<p>Create lesson plan</p>
				{/if}
			</button>
		</div>
	</div>
</div>
