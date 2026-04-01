<template>
  <section class="py-32 bg-surface-container-low overflow-hidden">
    <div class="max-w-7xl mx-auto px-8">
      <div class="grid grid-cols-1 md:grid-cols-12 gap-16 items-center">
        <!-- Left Column - Text Content -->
        <div class="md:col-span-5 space-y-12">
          <div>
            <h3 class="font-headline text-xs font-bold tracking-widest text-[#D44E98] mb-4 uppercase">
              LOKALIZACJA
            </h3>
            <h2 class="font-headline text-4xl font-extrabold text-on-surface leading-tight">
              Spokój, na który <br>zasługujesz.
            </h2>
            <p class="mt-8 text-secondary leading-relaxed text-base">
              Dom w Cyklamenach to nie tylko budynek. To starannie wybrana lokalizacja, która łączy bliskość miejskich udogodnień z kojącym dotykiem natury.
            </p>
          </div>
          
          <div class="space-y-10">
            <!-- Parks & Recreation -->
            <div class="flex gap-6 group">
              <div class="w-14 h-14 rounded-xl bg-white flex items-center justify-center text-[#D44E98] shadow-sm group-hover:shadow-md transition-shadow">
                <span class="material-symbols-outlined text-3xl">nature_people</span>
              </div>
              <div>
                <h4 class="font-headline font-bold text-on-surface text-lg">Parki i Rekreacja</h4>
                <p class="text-secondary text-sm mt-2">
                  Tylko 5 minut spacerem do najbliższego parku krajobrazowego.
                </p>
              </div>
            </div>
            
            <!-- Shopping -->
            <div class="flex gap-6 group">
              <div class="w-14 h-14 rounded-xl bg-white flex items-center justify-center text-[#D44E98] shadow-sm group-hover:shadow-md transition-shadow">
                <span class="material-symbols-outlined text-3xl">shopping_bag</span>
              </div>
              <div>
                <h4 class="font-headline font-bold text-on-surface text-lg">Zakupy i Usługi</h4>
                <p class="text-secondary text-sm mt-2">
                  Lokalne delikatesy i butiki w zasięgu ręki.
                </p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Right Column - Images -->
        <div class="md:col-span-7 relative">
          <div class="grid grid-cols-2 gap-6">
            <div class="pt-16">
              <img 
                alt="Modern Architecture Interior" 
                class="w-full aspect-[4/5] object-cover rounded-2xl shadow-2xl" 
                src="https://lh3.googleusercontent.com/aida-public/AB6AXuALDH0C_EtAUv8F2AirDKimRYVTTTo_hzohiao5dqxW6y6Ngl-PgtQ150gSuV0WvmnIq70aeiG-KkD7X6Do3AIHQNcaDbKYL4BtjJRB7I4tR09rMF1n0SX995zhNFXBkwUKGd_d7A7J6RApJlT-7PrEPr_loidTV4cpHPfNhC2ufaP70NogaWYznpDoidvMPRSXpUPIoZKfB9QIvpvO_g8aZZmTEdy2Otsap2MW65p8Ol0XqMnsTpfOxPVtwju5BzWrUxSOtkU6yuI"
              />
            </div>
            <div>
              <img 
                alt="Luxury Living Detail" 
                class="w-full aspect-[4/5] object-cover rounded-2xl shadow-2xl" 
                src="https://lh3.googleusercontent.com/aida-public/AB6AXuD0onJUAHwvh88y8Mrj5aHPH2GrTK4jOdy1lbc2uiufTRmgWIyYixFdYDpcMWM8yFeWBxoOts_5rFNG_0C51PUtmNt1ASQxbGjGqIVSCHs-lrulqf6FDAACh08SbV212qUxU6VFT-JTpAMn-YJEzcqv0lvi04HcZJCMqr_dr_bW2HOAZ262ocKKm08nLaOIymGLMnESspr1TSjFE9LUtZM1uTTEYi2UGd0pHAqIbNQUtlKVTRQxLB_MtrO627lVCClRLK7lQVEKKQ4"
              />
            </div>
          </div>
          <div class="absolute -right-20 -bottom-20 w-64 h-64 bg-primary/5 rounded-full blur-3xl"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
</script>
