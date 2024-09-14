<script lang="ts">
	import high1 from '$lib/assets/high_1.png';
	import high2 from '$lib/assets/high_2.png';
	import high3 from '$lib/assets/high_3.png';
	import junior from '$lib/assets/junior.png';

	import { RadioGroup, RadioItem } from '@skeletonlabs/skeleton';

	let value: number = 0;
</script>
<div class="container h-full mx-auto flex justify-center pt-8">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">校内マップ</h2>
		<RadioGroup>
			<RadioItem bind:group={value} name="justify" value={0}>高校1F</RadioItem>
			<RadioItem bind:group={value} name="justify" value={1}>高校2F</RadioItem>
			<RadioItem bind:group={value} name="justify" value={2}>高校3F</RadioItem>
			<RadioItem bind:group={value} name="justify" value={3}>中学</RadioItem>
		</RadioGroup>
		<div class="space-y-2 w-full h-72">
			{#if value === 0}
				<img src={high1} alt="高校棟1階" />
			{:else if value === 1}
				<img src={high2} alt="高校棟2階" />
			{:else if value === 2}
				<img src={high3} alt="高校棟3階" />
			{:else if value === 3}
				<img src={junior} alt="中学棟" />
			{/if}
			<!--<img src={birds_eye} alt="鳥瞰図">-->
		</div>
		<div class="pt-8 sm:pt-16 flex justify-center space-x-2">
			<a class="btn variant-filled" href="/course" rel="noreferrer" style="maegin: 0;">
				経路検索へ
			</a>
		</div>
	</div>
</div>

<style lang="postcss">
</style>
