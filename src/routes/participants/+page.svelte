<script lang="ts">
	import Icon from '@iconify/svelte';
	import { participants } from '$lib/participants';

	let searchTerm = '';
	let selectedCategory = '';

	function categoryOnClick(e: MouseEvent) {
		selectedCategory = (e.target as HTMLButtonElement).innerText;

		scrollToTop();
	}

	let top: HTMLElement;

	function scrollToTop() {
		top.scrollIntoView({
			behavior: 'smooth'
		});
	}

	$: filteredParticipants = participants.filter((participant) => {
		const matchesSearch =
			participant.name.includes(searchTerm) ||
			participant.at.includes(searchTerm) ||
			participant.by.includes(searchTerm) ||
			participant.category.join(' ').includes(searchTerm) ||
			participant.description.includes(searchTerm);

		const matchesCategory = selectedCategory
			? participant.category.includes(selectedCategory)
			: true;

		return matchesSearch && matchesCategory;
	});
</script>

<div class="container h-full mx-auto flex justify-center" bind:this={top}>
	<div class="w-full space-y-10 flex flex-col items-center">
		<div class="w-full xl:w-2/3 px-16 text-black mt-16 flex flex-col md:flex-row gap-4 mb-6">
			<input
				type="text"
				placeholder="検索"
				bind:value={searchTerm}
				class="w-full p-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-400 focus:border-transparent"
			/>

			<select
				bind:value={selectedCategory}
				on:change={scrollToTop}
				class="w-full md:w-1/2 p-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-400 focus:border-transparent"
			>
				<option value="">すべてのカテゴリ</option>
				{#each Array.from(new Set(participants.flatMap((p) => p.category))) as category}
					<option value={category}>{category}</option>
				{/each}
			</select>
		</div>

		<div class="m-6 my-8 grid grid-col-1 sm:grid-cols-2 xl:grid-cols-3 gap-4 lg:gap-8">
			{#each filteredParticipants as participant}
				<div class="p-4 flex-grow basis-96 border-t">
					<div class="flex justify-between p-2">
						<h3 class="text-xl sm:text-2xl">{participant.name}</h3>
						<div class="flex items-start">
							{#each participant.category as category}
								<button class="text-sm btn variant-filled mx-1" on:click={categoryOnClick}>
									{category}
								</button>
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
			{/each}
		</div>
		<div class="p-10"></div>
	</div>
</div>
