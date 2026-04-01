<template>
  <nav class="fixed top-0 z-50 w-full bg-white px-8 py-6 flex justify-between items-center border-b border-surface-variant/20">
    <div class="relative group cursor-pointer">
      <div class="text-xl font-headline font-extrabold tracking-tight text-on-surface uppercase">
        DOM W CYKLAMENACH
      </div>
      <div class="h-0.5 w-full bg-[#D44E98] mt-0.5"></div>
    </div>
    
    <div class="hidden md:flex gap-10 items-center">
      <a 
        class="font-label text-sm tracking-widest text-[#D44E98] border-b-2 border-[#D44E98] pb-1" 
        href="#"
      >
        Lokalizacja
      </a>
      <a 
        class="font-label text-sm tracking-widest text-secondary hover:text-[#D44E98] transition-colors duration-300" 
        href="#"
      >
        Galeria
      </a>
      <a 
        class="font-label text-sm tracking-widest text-secondary hover:text-[#D44E98] transition-colors duration-300" 
        href="#"
      >
        Kontakt
      </a>
      <button 
        class="primary-gradient-bg text-on-primary px-6 py-3 rounded-xl font-label text-xs font-bold tracking-widest transition-transform active:scale-95 duration-200"
      >
        Umów się na spotkanie
      </button>
    </div>
    
    <div class="md:hidden text-secondary">
      <span class="material-symbols-outlined">menu</span>
    </div>
  </nav>
</template>

<script setup lang="ts">
</script>
