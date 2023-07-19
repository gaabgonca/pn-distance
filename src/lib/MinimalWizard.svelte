<script lang="ts">
	import { RadioGroup, RadioItem } from '@skeletonlabs/skeleton';
	import { durations, rythms } from '../model/polvo';
	import { onMount } from 'svelte';
	import { add_styles } from 'svelte/internal';

	let size = 10,
		averageRythm = rythms.lentico,
		totalNumber = 0,
		averageDuration = durations.polvito;
        
    let body : HTMLElement
    let totalInput :  HTMLInputElement

    function getMetersTraveled(size: number, averageRythm: number, totalNumber: number, averageDuration: number): number {
        const sizeInMeters = size / 100;
        const insertsPerDust = averageRythm * averageDuration 
        const totalDistance = totalNumber * insertsPerDust * sizeInMeters;
        return totalDistance;

    }

	function getSizeText(size: number): string {
		if (size <= 10) {
			return 'Grande 👍';
		} else if (size <= 13) {
			return 'Más grande 👏';
		} else if (size <= 16) {
			return 'Enorme 😮';
		} else if (size <= 18) {
			return 'Gigante 🗿';
		} else {
			return 'Amenaza 🚀';
		}
	}

	function getDurationText(duration: number): string {
		if (duration === durations.polvito) {
			return 'Peor es nada';
		} else if (duration === durations.polvo) {
			return 'Si hubiera algo más sabroso que echar un polvo, se sabría';
		} else if (duration === durations.polvazo) {
			return 'Erda bien, así es que aguanta';
		} else if (duration === durations.huevera) {
			return 'Oiga, qué castigo';
		} else if (duration === durations.mondaquera) {
			return 'Hasta acá huele a caucho quemado';
		} else {
			return '';
		}
	}


	$: sizeText = getSizeText(size);
	$: durationText = getDurationText(averageDuration);
    $: totalDistanceInMeters = getMetersTraveled(size, averageRythm, totalNumber, averageDuration);
    $: totalDistanceInKilometers = totalDistanceInMeters / 1000;

    onMount(() => {
        if (!!totalInput) {
            totalInput.onfocus = (event) => {
                event.preventDefault();
                totalInput.scroll( {top: 2000, behavior:'smooth' });
            }
        }
    })
</script>

<section bind:this={body} class="w-screen md:w-full h-screen flex flex-col grow items-start overflow-auto justify-start px-4 py-20">
	<div class="w-full h-fit p-4 surface-700 mb-80">
        <h1 class="text-4xl">¿Cuánto ha recorrido mi pn?</h1>
		<h2 class="text-base">Cálculalo aquí y ahora, de gratis (no guardamos información, esto es pura recocha)</h2>
        <div class="h-8 w-full" />
		<label for="size" class="label w-full">
			<span class="question">Tamaño del equipo en cm</span>
			<span class="flex flex-row w-full items-center justify-between px-0">
				<input type="range" class="flex w-72" bind:value={size} min="3" max="25" />
				<span class="w-max flex line-clamp-1">{size} cm</span>
			</span>
			<p class="w-full mx-auto text-center comment">{sizeText}</p>
		</label>
		<div class="h-8 w-full" />
		<span class="question">Duración promedio de los polvos</span>
		<RadioGroup class="flex flex-col w-full items-center justify-center">
			<RadioItem
				class="flex w-full"
				name="averageDuration"
				bind:group={averageDuration}
				value={durations.polvito}>Polvito (0 a 5 mins)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageDuration"
				bind:group={averageDuration}
				value={durations.polvo}>Polvo (5 a 15 mins)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageDuration"
				bind:group={averageDuration}
				value={durations.polvazo}>Polvazo (15 a 30 mins)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageDuration"
				bind:group={averageDuration}
				value={durations.huevera}>Huevera (30 a 45 mins)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageDuration"
				bind:group={averageDuration}
				value={durations.mondaquera}>Mondaquera (45 a 60 mins)</RadioItem
			>
		</RadioGroup>
		<p class="w-full mx-auto text-center comment">{durationText}</p>
        <div class="h-8 w-full" />
		<span class="question label">Ritmo promedio de los polvos (metidas por minuto)</span>
		<RadioGroup class="flex flex-col w-full items-center justify-center">
			<RadioItem
				class="flex w-full"
				name="averageDuration"
				bind:group={averageRythm}
				value={rythms.lentico}>Lentico (30 ↑ por minuto)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageRythm"
				bind:group={averageRythm}
				value={rythms.segunda}>En segunda (45 ↑ por minuto)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageRythm"
				bind:group={averageRythm}
				value={rythms.cuarta}>En cuarta (70 ↑ por minuto)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageRythm"
				bind:group={averageRythm}
				value={rythms.sexta}>En sexta (100 ↑ por minuto)</RadioItem
			>
			<RadioItem
				class="flex w-full"
				name="averageRythm"
				bind:group={averageRythm}
				value={rythms.coser}>Máquina de coser (130 ↑ por minuto)</RadioItem
			>
            <RadioItem
				class="flex w-full"
				name="averageRythm"
				bind:group={averageRythm}
				value={rythms.embale}>Embale (160 ↑ por minuto)</RadioItem
			>
		</RadioGroup>
        <div class="h-8 w-full" />
		<label for="totalNumber label" class="label w-full">
			<span class="question">Número estimado de polvos</span>
				<input bind:this={totalInput} class="flex w-full input text-right text-xl" bind:value={totalNumber} type="number" inputmode="numeric"/>
		</label>
		<div class="h-8 w-full" />
        {#if (totalDistanceInMeters < 1000)}
        <span>Según mis cuentas, tu pn ha recorrido </span>
        <p class="text-2xl font-bold text-center my-4 ">{totalDistanceInMeters} metros </p> 
        {:else}
        <span>Según mis cuentas, tu pn ha recorrido</span>
        <p class="text-2xl font-bold">{totalDistanceInKilometers} kilómetros</p>
        {/if}
        
	</div>
</section>


<style lang="postcss">
	.surface-700 {
		background-color: rgb(var(--color-surface-700));
		@apply rounded-xl;
	}
	.question {
		@apply text-lg;
		@apply font-bold;
	}
	.comment {
		color: rgb(var(--color-primary-300));
	}
</style>
