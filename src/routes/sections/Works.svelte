<script lang="ts">
  import { fade } from 'svelte/transition';
</script>

<section id="works" class="h-screen flex flex-col justify-center items-center px-6">
  <div transition:fade={{ duration: 600 }} class="max-w-4xl">
    <p class="text-xl text-gray-700 leading-relaxed">
      私が運営している
      <span class="font-semibold text-indigo-600"><a href="https://github.com/nobody-artifact" target="_blank">Nobody Artifact</a></span> は、
      <span class="font-semibold">企業向けAIシステム開発</span> に特化したプロジェクトです。
      私たちは単なるAIの導入ではなく、企業の課題に直結したAI戦略を設計し、
      現場に根ざした実用性のあるAIソリューションを構築します。
    </p>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mt-10">
      <!-- AIアーキテクチャ設計 -->
      <div class="p-6 bg-white shadow-xl rounded-lg border border-gray-200">
        <h3 class="text-2xl font-semibold mb-3">精密なAIアーキテクチャ設計</h3>
        <p class="text-gray-600 leading-relaxed">
          AIは単なるツールではなく、ビジネスのエンジンです。
          データ構造・アルゴリズム設計・クラウドインフラを総合的に考慮し、
          スケーラブルで拡張性のあるAIシステムを提供します。
        </p>
      </div>

      <!-- AIの一気通貫開発 -->
      <div class="p-6 bg-white shadow-xl rounded-lg border border-gray-200">
        <h3 class="text-2xl font-semibold mb-3">AIのフルスタック開発</h3>
        <p class="text-gray-600 leading-relaxed">
          AIのモデル設計から、バックエンド・フロントエンド・データパイプラインまで、
          すべてを一気通貫で開発し、企業がすぐに活用できる形に仕上げます。
        </p>
      </div>
    </div>

    <div class="text-center">

      <button class="mt-12 px-6 py-3 bg-indigo-600 text-white rounded-full hover:bg-indigo-500 transition text-lg">
        事例を見る
      </button>
    </div>
  </div>
</section>
