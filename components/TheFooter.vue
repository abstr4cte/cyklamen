<template>
  <footer class="bg-surface-container-low border-t border-surface-variant/20">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-16 px-8 py-24 max-w-7xl mx-auto">
      <!-- Brand Column -->
      <div class="space-y-8">
        <div class="relative inline-block">
          <div class="text-xl font-headline font-extrabold text-on-surface uppercase">
            DOM W CYKLAMENACH
          </div>
          <div class="h-0.5 w-full bg-[#D44E98] mt-0.5"></div>
        </div>
        <p class="font-body text-secondary leading-relaxed text-sm">
          Tworzymy miejsca, które inspirują do lepszego życia. Architektura z duszą, zaprojektowana dla Twojego komfortu.
        </p>
      </div>
      
      <!-- Navigation Column -->
      <div class="space-y-8">
        <h4 class="font-label text-xs font-bold tracking-widest text-[#D44E98] uppercase">
          NAWIGACJA
        </h4>
        <ul class="space-y-5">
          <li>
            <a class="font-body text-sm text-secondary hover:text-[#D44E98] transition-colors" href="#">
              Dane kontaktowe
            </a>
          </li>
          <li>
            <a class="font-body text-sm text-secondary hover:text-[#D44E98] transition-colors" href="#">
              Lokalizacja na mapie
            </a>
          </li>
          <li>
            <a class="font-body text-sm text-secondary hover:text-[#D44E98] transition-colors" href="#">
              Polityka prywatności
            </a>
          </li>
        </ul>
      </div>
      
      <!-- Contact Info Column -->
      <div class="space-y-8">
        <h4 class="font-label text-xs font-bold tracking-widest text-[#D44E98] uppercase">
          BIURO SPRZEDAŻY
        </h4>
        <div class="space-y-5 font-body text-sm text-secondary">
          <div class="flex items-start gap-4">
            <span class="material-symbols-outlined text-xl text-[#D44E98]">location_on</span>
            <span class="leading-tight">ul. Kwiatowa 12,<br>00-001 Warszawa</span>
          </div>
          <div class="flex items-center gap-4">
            <span class="material-symbols-outlined text-xl text-[#D44E98]">call</span>
            <span>+48 123 456 789</span>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Bottom Bar -->
    <div class="max-w-7xl mx-auto px-8 py-12 border-t border-surface-variant/20 flex flex-col md:flex-row justify-between items-center gap-8">
      <p class="font-body text-[13px] text-secondary">
        © 2024 Dom w Cyklamenach. Wszelkie prawa zastrzeżone.
      </p>
      <div class="flex gap-8 text-secondary/60">
        <span class="material-symbols-outlined hover:text-[#D44E98] cursor-pointer transition-colors text-xl">
          public
        </span>
        <span class="material-symbols-outlined hover:text-[#D44E98] cursor-pointer transition-colors text-xl">
          mail
        </span>
        <span class="material-symbols-outlined hover:text-[#D44E98] cursor-pointer transition-colors text-xl">
          share
        </span>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
</script>
