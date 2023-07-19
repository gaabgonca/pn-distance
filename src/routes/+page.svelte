<script>
	import WizardFactory from '$lib/WizardFactory.svelte';
import { RadioGroup, RadioItem } from '@skeletonlabs/skeleton';
	let hasStarted = true;
	let mode = 0
</script>
<div class="h-full md:w-2/5 flex justify-center items-center w-full px-4">
	{#if !hasStarted}
	<div class="space-y-4 text-center flex flex-col items-center">
		<h1 class="text-4xl">¿Cuánto ha recorrido mi pn?</h1>
		<h2 class="text-base">Cálculalo aquí y ahora, de gratis (no guardamos información, esto es pura recocha)</h2>
		<div class="vspacer"></div>
		<h1 class="text-2xl">Te voy a hacer unas preguntas sobre tu recorrido. Escoge cómo quieres hacer el cálculo</h1>
		<div class="vspacer"></div>
		<RadioGroup class="flex-col w-full">
			<RadioItem value={0} bind:group={mode} name="mode">Mínimo (número total de polvos y detalles promedio aproximados)</RadioItem>
			<RadioItem value={1} bind:group={mode} name="mode">Sencillo (número de polvos por pareja y detalles promedio aproximados)</RadioItem>
			<RadioItem value={2} bind:group={mode} name="mode">Avanzado (número de polvos y detalles por pareja)</RadioItem>
		</RadioGroup>
		<div class="vspacer"></div>
		<button class="btn btn-xl variant-filled" on:click={() => (hasStarted = true)}>Iniciar</button>
	</div>
	{:else}
	<WizardFactory bind:hasStarted={hasStarted} bind:mode={mode}/>
	{/if}
</div>

<style lang="postcss">
	.vspacer {
		width: 100%;
		height: 1rem;
	}
</style>
