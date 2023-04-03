<script>
	import LoadingIndicator from './Loading.svelte';

	/**
	 * @type string
	 */
	export let LearningStyleType;
	/**
	 * @type Array<string>
	 */
	export let selectedCategories;
	/**
	 * @type string
	 */
	export let specificDescriptors;
	/**
	 * @type Boolean
	 */
	export let loading;

	const categoryTypes = [
  'Objetivos de la clase',
  'Actividades',
  'Evaluación',
  'Materiales requeridos',
  'Recursos adicionales',
  'Tiempo estimado',
  'Habilidades a desarrollar',
  'Competencias a desarrollar',
  'Estrategias de enseñanza',
  'Métodos de evaluación',
  'Requisitos previos',
  'Evaluación del aprendizaje',
  'Retroalimentación',
  'Aprendizaje colaborativo',
  'Aprendizaje autónomo',
  'Enfoque interdisciplinario',
  'Aprendizaje basado en proyectos',
  'Aprendizaje basado en problemas',
  'Aprendizaje activo',
  'Aprendizaje en línea',
  'Aprendizaje híbrido'
];

	let LearningStyleTypes = [
  { value: 'visual', title: 'Visual' },
  { value: 'auditivo', title: 'Auditivo' },
  { value: 'lectura/escritura', title: 'Lectura/Escritura' },
  { value: 'kinestésico', title: 'Kinestésico' },
  { value: 'sin preferencia', title: 'Sin Preferencia' }
];

</script>

<div class="pt-6 md:pt-10 text-slate-200">
	<div>
		<div class="mb-8">
			<div class="mb-4 font-semibold text-lg">Elige un estilo de aprendizaje</div>
			<div class="flex items-center">
				{#each LearningStyleTypes as type (type.value)}
					<button
						on:click={() => {
							LearningStyleType = type.value;
						}}
						class={`${
							LearningStyleType === type.value ? 'bg-pink-600/40' : ''
						} text-slate-200 font-bold mr-2 text-sm mt-2 py-2 px-4 rounded-full border border-pink-600`}
					>
						{type.title}
					</button>
				{/each}
			</div>
		</div>
		<div>
			<div class="mb-4 font-semibold text-lg">
				Selecciona los modulos de tu planeación de clase.
			</div>
			<div class="flex items-center flex-wrap">
				{#each categoryTypes as category}
					<label
						class={`${
							selectedCategories.includes(category) ? 'bg-pink-600/40' : ''
						} text-slate-200 font-bold mr-2 mt-2 text-sm py-2 px-4 rounded-full border border-pink-600`}
					>
						<input
							class="hidden"
							type="checkbox"
							bind:group={selectedCategories}
							name="categories"
							value={category}
						/>
						{category}
					</label>
				{/each}
			</div>
		</div>
		<div class="mt-8">
			<div class="mb-4 font-semibold text-lg">
				Elige un tema de tu elección para generar la planeación de clase.
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
					<p>Generar mi clase</p>
				{/if}
			</button>
		</div>
	</div>
</div>
