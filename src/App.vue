<script setup>
import { ref } from 'vue'
import SearchInput from './components/SearchInput.vue'
import WeatherCard from './components/WeatherCard.vue'
const places = ref([])

const addPlace = (data) => {
  places.value.push(data)
}

const deletePlace = (name) => {
  if (confirm('Biztos Törlöd?')) {
    places.value = places.value.filter((p) => p.location.name !== name)
  }
}
</script>

<template>
  <main>
    <div class="text-center mb-4">
      {{
        new Date().toLocaleString('hu', {
          weekday: 'long',
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        })
      }}
    </div>

    <div>
      <SearchInput @place-data="addPlace" />
    </div>

    <div class="grid grid-cols-1 gap-2">
      <div v-for="(place, idx) in places" :key="idx">
        <WeatherCard :place="place" @delete-place="deletePlace" />
      </div>
    </div>
  </main>
</template>
