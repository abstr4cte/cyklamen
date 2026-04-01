<template>
  <section class="py-32 bg-surface">
    <div class="max-w-7xl mx-auto px-8">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-20">
        <!-- Standard -->
        <div class="text-center space-y-6">
          <div class="flex justify-center mb-8">
            <div class="w-16 h-16 rounded-2xl bg-primary/5 flex items-center justify-center text-[#D44E98]">
              <span class="material-symbols-outlined text-4xl" style="font-variation-settings: 'FILL' 1">verified</span>
            </div>
          </div>
          <h3 class="font-headline text-xl font-bold text-on-surface tracking-tight">Standard</h3>
          <p class="text-secondary text-sm leading-relaxed max-w-xs mx-auto">
            Najwyższa jakość materiałów i nowoczesne systemy energooszczędne w każdym domu.
          </p>
        </div>

        <!-- Lokalizacja -->
        <div class="text-center space-y-6 border-x border-surface-variant/30 px-8">
          <div class="flex justify-center mb-8">
            <div class="w-16 h-16 rounded-2xl bg-primary/5 flex items-center justify-center text-[#D44E98]">
              <span class="material-symbols-outlined text-4xl" style="font-variation-settings: 'FILL' 1">location_on</span>
            </div>
          </div>
          <h3 class="font-headline text-xl font-bold text-on-surface tracking-tight">Lokalizacja</h3>
          <p class="text-secondary text-sm leading-relaxed max-w-xs mx-auto">
            Znakomite skomunikowanie z centrum przy zachowaniu pełnej prywatności i ciszy.
          </p>
        </div>

        <!-- Design -->
        <div class="text-center space-y-6">
          <div class="flex justify-center mb-8">
            <div class="w-16 h-16 rounded-2xl bg-primary/5 flex items-center justify-center text-[#D44E98]">
              <span class="material-symbols-outlined text-4xl" style="font-variation-settings: 'FILL' 1">architecture</span>
            </div>
          </div>
          <h3 class="font-headline text-xl font-bold text-on-surface tracking-tight">Design</h3>
          <p class="text-secondary text-sm leading-relaxed max-w-xs mx-auto">
            Minimalistyczna bryła i funkcjonalne wnętrza tworzące idealną przestrzeń do życia.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
</script>
