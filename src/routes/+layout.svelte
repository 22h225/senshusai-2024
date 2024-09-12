<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';

	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';
	import { storePopup } from '@skeletonlabs/skeleton';
	storePopup.set({ computePosition, autoUpdate, flip, shift, offset, arrow });
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-normal uppercase pl-2 sm:pl-6 md:text-xl">
					<a href="/" rel="noreferrer"> 2024 県立千葉千秋祭 </a>
				</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<div class="grid grid-cols-2 gap-2">
					<a
						class="btn btn-sm variant-ghost-surface"
						href="https://cms1.chiba-c.ed.jp/chiba-h/"
						target="_blank"
						rel="noreferrer"
					>
						<span class="hidden max-sm:inline-block">HP</span>
						<span class="hidden pr-2 sm:inline-block">千葉高校ホームページ</span>
					</a>
					<a
						class="btn btn-sm variant-ghost-surface"
						href="https://github.com/22h225/senshusai-2024"
						target="_blank"
						rel="noreferrer"
					>
						<span class="hidden max-md:inline-block">GitHub</span>
						<span class="hidden pr-2 md:inline-block">GitHubでソースコードを見る</span>
					</a>
				</div>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
