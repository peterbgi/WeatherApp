<script setup>
defineProps({
  place: Object
})
</script>

<template>
  <div
    class="absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8"
  >
    <div class="flex justify-end mb-10">
      <button @click="$emit('close-info')" class="p-1">
        <i class="fa-solid fa-xmark text-xl"></i>
      </button>
    </div>

    <div class="flex items-center justify-between gap-6 mb-20">
      <div class="text-center flex-1">
        <i class="fa-solid fa-wind mb text-2xl"></i>
        <p class="text-xl font-bold"><small>Szélsebesség: </small> {{ place.current.wind_kph }}</p>
      </div>
      <div class="text-center flex-1">
        <i class="fa-solid fa-droplet mb text-2xl"></i>
        <p class="text-xl font-bold"><small>Páratartalom: </small> {{ place.current.humidity }}%</p>
      </div>
      <div class="text-center flex-1">
        <i class="fa-solid fa-umbrella mb text-2xl"></i>
        <p class="text-xl font-bold"><small>Csapadék: </small> {{ place.current.precip_mm }}mm</p>
      </div>
    </div>
    <div class="flex items-center justify-between gap-6 mb-10">
      <div class="text-center flex-1">
        <i class="fa-solid fa-fan mb text-2xl"></i>
        <p class="text-xl font-bold"><small>Szélirány: </small> {{ place.current.wind_dir }}Í</p>
      </div>
      <div class="text-center flex-1">
        <i class="fa-solid fa-temperature-half mb text-2xl"></i>
        <p class="text-xl font-bold">
          <small>Hőérzet: </small>
          {{ Math.round(place.current.feelslike_c) }}
        </p>
      </div>
      <div class="text-center flex-1">
        <i class="fa-solid fa-sun mb text-2xl"></i>
        <p class="text-xl font-bold">
          <small>UV Index: </small>
          {{ place.current.uv }}
        </p>
      </div>
    </div>
    <!-- Last update and delete -->
    <div class="flex justify-between items-center">
      <h3 class="text-slate-900/50">
        <small>Utoljára frissíítve: </small>
        {{ place.current.last_updated }}
      </h3>
      <button @click="$emit('delete-place')">
        <i class="fa-solid fa-trash"></i>
      </button>
    </div>
  </div>
</template>
