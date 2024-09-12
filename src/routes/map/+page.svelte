<script lang="ts">
	import high1 from '$lib/assets/high_1.png';
	import high2 from '$lib/assets/high_2.png';
	import high3 from '$lib/assets/high_3.png';
	import junior from '$lib/assets/junior.png';
	import birds_eye from '$lib/assets/birds_eye.png';

	import { RadioGroup, RadioItem } from '@skeletonlabs/skeleton';

	let value: number = 0;
</script>

<!-- YOU CAN DELETE EVERYTHING IN THIS PAGE -->

<div class="container h-full mx-auto flex justify-center pt-8">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">校内マップ</h2>
		<RadioGroup>
			<RadioItem bind:group={value} name="justify" value={0}>高校1F</RadioItem>
			<RadioItem bind:group={value} name="justify" value={1}>高校2F</RadioItem>
			<RadioItem bind:group={value} name="justify" value={2}>高校3F</RadioItem>
			<RadioItem bind:group={value} name="justify" value={3}>中学</RadioItem>
		</RadioGroup>
		<div class="space-y-2 w-full h-48">
			{#if value === 0}
				<img src={high1} alt="高校棟1階" />
				<!-- <table>
					<tr>
						<th>番号</th>
						<th>団体名</th>
						<th>企画名</th>
						<th>ジャンル</th>
						<th>場所</th>
					</tr>
					<tr>
						<td>1</td>
						<td>3-A</td>
						<td>ラプンツェル</td>
					</tr>
				</table> -->
			{:else if value === 1}
				<img src={high2} alt="高校棟2階" />
			{:else if value === 2}
				<img src={high3} alt="高校棟3階" />
			{:else if value === 3}
				<img src={junior} alt="中学棟" />
			{/if}
			<!--<img src={birds_eye} alt="鳥瞰図">-->
		</div>
	</div>
</div>

<style lang="postcss">
</style>
