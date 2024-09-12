<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center pt-6">
		<p class="text-2xl sm:text-4xl kaisei-harunoumi-regular">Welcome to</p>
		<!-- Animated Logo -->
		<figure>
			<section class="img-bg" />
			<h1 class="w-full text-7xl sm:text-9xl kaisei-harunoumi-regular content-center">千秋祭</h1>
			<p class="text-xl sm:text-3xl kaisei-harunoumi-regular pt-4">9月14日(土) 9時30分～15時</p>
			<p class="text-xl sm:text-3xl kaisei-harunoumi-regular">9月15日(日) 9時30分～14時45分</p>
		</figure>
		<div class="pt-8 sm:pt-16 flex justify-center space-x-2">
			<a class="btn variant-filled" href="/about" rel="noreferrer">
				詳しく知る
			</a>
		</div>
		<div class="space-y-2 pb-4">
			<p class="text-xl">ページ一覧</p>
			<div class="border rounded p-4">
				<p class="p-0.5">
					<a href="participants/" rel="noreferrer"> 参加団体一覧 </a>
				</p>
				<p class="p-0.5">
					<a href="map/" rel="noreferrer"> 校内マップ </a>
				</p>
			</div>
		</div>
	</div>
</div>

<style lang="postcss">
	figure {
		@apply flex relative flex-col;
	}
	figure h1,
	.img-bg {
		@apply w-full h-64 max-sm:h-20;
	}
	.img-bg {
		@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
		animation:
			pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,
			glow 5s linear infinite;
	}
	@keyframes glow {
		0% {
			@apply bg-primary-400/50;
		}
		33% {
			@apply bg-secondary-400/50;
		}
		66% {
			@apply bg-tertiary-400/50;
		}
		100% {
			@apply bg-primary-400/50;
		}
	}
	@keyframes pulse {
		50% {
			transform: scale(1.5);
		}
	}
</style>
