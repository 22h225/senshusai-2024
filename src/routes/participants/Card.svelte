<script lang="ts">
	import type { Participant } from '$lib/participants';
	import Icon from '@iconify/svelte';
	export let participant: Participant;
</script>

<div class="p-4 flex-grow basis-96">
	<div class="flex justify-between">
		<h3 class="text-2xl">{participant.name}</h3>
		<div class="flex items-start">
			{#each participant.category as category}
				<p class="text-sm btn variant-filled mx-1">
					{category}
				</p>
			{/each}
		</div>
	</div>
	<div>
		<div class="flex text-sm gap-4">
			<div class="flex items-center">
				<Icon icon="mdi:user" />
				<p class="">{participant.by}</p>
			</div>
			<div class="flex items-center">
				<Icon icon="mdi:map-marker" />
				<p class="">{participant.at}</p>
			</div>
		</div>
		<p class="p-4">{participant.description}</p>
	</div>
</div>

<style lang="scss">
</style>
