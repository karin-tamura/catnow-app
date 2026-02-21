<script setup>
// WordPressからデータを取得
const { data: posts } = await useFetch('https://calmnote.s2-tastewp.com/wp-json/wp/v2/posts?_embed')
</script>

<template>
  <div v-if="posts" class="min-h-screen bg-slate-50 font-sans text-slate-900 pb-20">
    <header class="bg-white/80 backdrop-blur-md border-b sticky top-0 z-10 py-4 shadow-sm">
      <h1 class="text-2xl font-black text-orange-500 tracking-tighter italic text-center">CatNow</h1>
    </header>

    <main class="max-w-xl mx-auto p-4 flex flex-col items-center space-y-12">
      
      <article 
        v-for="post in posts" 
        :key="post.id" 
        class="w-full bg-white rounded-[2.5rem] shadow-xl shadow-orange-100/50 border border-slate-100 overflow-hidden"
      >
        <div class="w-full bg-slate-50 border-b border-slate-50 flex items-center justify-center">
          <img 
            :src="post._embedded?.['wp:featuredmedia']?.[0]?.source_url" 
            class="w-full h-auto block" 
            alt="ゆずちゃん"
          />
        </div>
        
        <div class="p-8">
          <div class="flex items-center gap-2 mb-4">
            <span class="w-2 h-2 bg-orange-500 rounded-full animate-pulse"></span>
            <span class="text-xs font-bold text-orange-500 uppercase tracking-widest">Yuzu Insight</span>
          </div>

          <h2 class="text-2xl font-extrabold mb-4 leading-tight text-slate-800" v-html="post.title.rendered"></h2>
          
          <div class="text-slate-600 leading-relaxed mb-8 prose prose-slate max-w-none 
                      prose-img:rounded-2xl prose-video:w-full prose-video:rounded-2xl prose-video:aspect-video" 
               v-html="post.content.rendered">
          </div>
          
          <div class="flex items-center justify-between border-t border-slate-50 pt-6">
            <div class="text-slate-400 text-xs font-medium">
              {{ new Date(post.date).toLocaleDateString('ja-JP') }}
            </div>
            <div class="bg-orange-50 text-orange-600 text-[10px] font-black px-3 py-1 rounded-full border border-orange-100">
              CAT REPORT
            </div>
          </div>
        </div>
      </article>

    </main>

    <footer class="text-center py-10">
      <p class="text-slate-300 text-sm font-serif italic">~ No Yuzu, No Life ~</p>
    </footer>
  </div>
</template>

<style>
/* 動画（YouTubeや直接アップロード）がはみ出さないための魔法 */
.prose video, .prose iframe {
  width: 100% !important;
  border-radius: 1rem;
  box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1);
}
</style>