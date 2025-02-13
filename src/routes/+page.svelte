<script lang="ts">
  import { fade } from 'svelte/transition';

  // 章の情報を配列で管理
  const sections = [
    { title: "Works", link: "#works", content: "todo" },
  ];

  let currentSection = 0;
  let isAnimating = false;

  // スクロールで遷移
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

<!-- 全体コンテナ -->
<div class="h-screen w-screen flex flex-col relative" on:wheel={handleWheel}>

  <!-- ヘッダー（ナビゲーション） -->
  <header class="relative">
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

  <!-- メインエリア -->
  <div class="flex flex-1 relative">
    <!-- 現在の章名 -->
    <div class="relative w-20 flex flex-col items-center justify-center">
      <div class="absolute left-3 top-1/2 transform -rotate-90 -translate-y-1/2 text-lg">
        {sections[currentSection].title}
      </div>
    </div>

    <!-- コンテンツ部分（フェード遷移） -->
    <div class="flex-1 flex justify-center items-center relative">
      {#key currentSection}
        <div
          transition:fade={{ duration: 600 }}
          class="absolute inset-0 flex flex-col justify-center items-center">
          <p class="text-xl text-center mt-4">
          {sections[currentSection].content}
          </p>
        </div>
      {/key}
    </div>
  </div>

  <!-- フッター -->
  <footer class="relative bg-white p-3 text-center">
    <p>&copy; {new Date().getFullYear()} kakeru.io</p>
  </footer>
</div>
