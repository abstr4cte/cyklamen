<template>
  <section class="relative min-h-screen flex items-center justify-start overflow-hidden mt-[88px]">
    <div class="absolute inset-0 z-0">
      <video 
        class="w-full h-full object-cover" 
        autoplay 
        loop 
        muted 
        playsinline
      >
        <source src="/assets/layout/banner.mp4" type="video/mp4" />
      </video>
    </div>
    
    <div class="relative z-10 w-full max-w-7xl px-8 md:px-16">
      <div class="w-full max-w-[480px] hero-glass-box p-10 md:p-14 rounded-xl shadow-xl">
        <h1 class="font-headline text-4xl md:text-5xl font-extrabold tracking-tight text-on-surface mb-6 leading-[1.1]">
          Twój nowy rozdział <br><span class="text-[#D44E98]">zaczyna się tutaj.</span>
        </h1>
        <p class="text-on-surface/80 text-sm md:text-base mb-10 leading-relaxed font-semibold">
          Odkryj harmonię nowoczesnej architektury i natury. Przestrzeń zaprojektowana z myślą o Twoim komforcie i spokoju ducha.
        </p>
        <div class="flex gap-4">
          <button class="primary-gradient-bg text-on-primary px-10 py-5 rounded-lg font-label text-[12px] font-bold tracking-widest shadow-xl shadow-primary/30 uppercase transition-all duration-300 hover:scale-105 hover:brightness-110 active:scale-95">
            ZOBACZ PROJEKT
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
</script>
