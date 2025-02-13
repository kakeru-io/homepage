<script lang="ts">
	import { fade } from 'svelte/transition';
	import Works from './sections/Works.svelte';
	import Products from './sections/Products.svelte';

	// 章の情報を配列で管理
	const sections = [
		{ title: 'WORKS', link: '#works', component: Works },
		{ title: 'PRODUCTS', link: '#products', component: Products },
	];

	const maxSectionTitleWidth = sections.reduce((max, section) => Math.max(max, section.title.length), 0) + 2;
	const titleWidth = (title: string) => maxSectionTitleWidth - title.length;

	let currentSection = 0;
	let isAnimating = false;

	function handleWheel(event: WheelEvent) {
		if (isAnimating) return;

		if (event.deltaY > 0 && currentSection < sections.length - 1) {
			isAnimating = true;
			currentSection += 1;
		} else if (event.deltaY < 0 && currentSection > 0) {
			isAnimating = true;
			currentSection -= 1;
		}

		setTimeout(() => isAnimating = false, 600);
	}
</script>

<style lang="postcss">
    :global(body) {
        @apply m-0 p-0 overflow-hidden bg-gray-50 text-gray-900;
    }

    .menu-scroll {
        overflow-x: auto;
        white-space: nowrap;
        scrollbar-width: none;
    }

    .menu-scroll::-webkit-scrollbar {
        display: none;
    }
</style>

<!-- メインコンテナ -->
<div class="h-screen w-screen flex flex-col relative" on:wheel={handleWheel}>
	<!-- ヘッダー -->
	<header class="relative w-full">
		<div class="flex justify-between items-center max-w-6xl mx-auto px-4 py-3">
			<div class="font-bold text-xl">kakeru.io</div>
			<nav class="menu-scroll flex space-x-6 px-2">
				{#each sections as section, i}
					<button
						class="hover:text-indigo-600 text-lg transition-colors"
						on:click={() => currentSection = i}>
						{section.title}
					</button>
				{/each}
			</nav>
		</div>
	</header>

	<!-- メインコンテンツ -->
	<div class="flex flex-1 max-w-6xl mx-auto w-full relative">
		<!-- 左のセクションタイトル -->
		<div class="w-20 flex items-center justify-center relative">
			<div
				class="text-lg border-r border-gray-500 border-dashed px-2 text-center"
				style="writing-mode: vertical-rl; text-orientation: upright; letter-spacing: 1.0em">
				{#each Array.from({ length: titleWidth(sections[currentSection].title) / 2 }) as _, i}&nbsp;{/each} {sections[currentSection].title}{#each Array.from({ length: titleWidth(sections[currentSection].title) / 2 }) as _, i}&nbsp;{/each}
			</div>
		</div>

		<!-- メインコンテンツ表示 -->
		<div class="flex-1 flex justify-center items-center relative">
			{#key currentSection}
				<div
					transition:fade={{ duration: 600 }}
					class="absolute inset-0 flex flex-col justify-center items-center w-full">
					<svelte:component this={sections[currentSection].component} />
				</div>
			{/key}
		</div>
	</div>

	<!-- フッター -->
	<footer class="relative w-full">
		<div class="max-w-6xl mx-auto p-3 text-center text-sm" style="color: gray">
			<p style="font-size: 12px">
				<span>&copy; {new Date().getFullYear()} <a href="https://kakeru.io/">kakeru.io</a> - Powered by bootware</span>
			</p>
		</div>
	</footer>
</div>
