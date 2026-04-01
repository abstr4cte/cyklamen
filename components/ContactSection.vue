<template>
  <section class="py-32 md:py-48 bg-surface">
    <div class="max-w-4xl mx-auto px-8">
      <div class="bg-white p-12 md:p-24 rounded-2xl shadow-2xl shadow-on-surface/5 border border-surface-variant/30 text-center">
        <h2 class="font-headline text-4xl font-extrabold text-on-surface mb-6">
          Zrób pierwszy krok
        </h2>
        <p class="text-secondary mb-16 text-lg">
          Zostaw swoje dane, a nasz doradca skontaktuje się z Tobą w ciągu 24 godzin.
        </p>
        
        <form class="grid grid-cols-1 md:grid-cols-2 gap-12 text-left" @submit.prevent="handleSubmit">
          <!-- Name Input -->
          <div class="space-y-3">
            <label class="font-label text-xs tracking-widest text-secondary uppercase font-bold">
              Imię i Nazwisko
            </label>
            <input 
              v-model="formData.name"
              class="w-full bg-transparent border-0 border-b-2 border-outline-variant/30 focus:ring-0 focus:border-[#D44E98] transition-colors py-4 px-0 text-on-surface placeholder:text-surface-dim font-medium" 
              placeholder="Jan Kowalski" 
              type="text"
            />
          </div>
          
          <!-- Phone Input -->
          <div class="space-y-3">
            <label class="font-label text-xs tracking-widest text-secondary uppercase font-bold">
              Telefon
            </label>
            <input 
              v-model="formData.phone"
              class="w-full bg-transparent border-0 border-b-2 border-outline-variant/30 focus:ring-0 focus:border-[#D44E98] transition-colors py-4 px-0 text-on-surface placeholder:text-surface-dim font-medium" 
              placeholder="+48 000 000 000" 
              type="tel"
            />
          </div>
          
          <!-- Message Textarea -->
          <div class="md:col-span-2 space-y-3 pt-6">
            <label class="font-label text-xs tracking-widest text-secondary uppercase font-bold">
              Wiadomość (opcjonalnie)
            </label>
            <textarea 
              v-model="formData.message"
              class="w-full bg-transparent border-0 border-b-2 border-outline-variant/30 focus:ring-0 focus:border-[#D44E98] transition-colors py-4 px-0 text-on-surface placeholder:text-surface-dim font-medium" 
              placeholder="Jak możemy Ci pomóc?" 
              rows="2"
            ></textarea>
          </div>
          
          <!-- Submit Button -->
          <div class="md:col-span-2 pt-12">
            <button 
              class="w-full primary-gradient-bg text-on-primary py-6 rounded-xl font-label font-bold tracking-[0.25em] shadow-xl shadow-primary/30 active:scale-[0.98] transition-all text-xs" 
              type="submit"
            >
              ZAMAWIAM KONTAKT
            </button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { reactive } from 'vue'

const formData = reactive({
  name: '',
  phone: '',
  message: ''
})

const handleSubmit = () => {
  console.log('Form submitted:', formData)
  // Handle form submission logic here
}
</script>
