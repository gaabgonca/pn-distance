<script lang="ts">
	import MinimalWizard from "./MinimalWizard.svelte";

    export let mode : number;
    export let hasStarted: boolean;
</script>

<div > 
    {#if mode === 0}
    <MinimalWizard/>
    {:else if mode === 1}
    <h1 class="text-xl">Sencillo</h1>
    {:else if mode === 2}
    <h1 class="text-xl">Avanzado</h1>
    {/if}

</div>