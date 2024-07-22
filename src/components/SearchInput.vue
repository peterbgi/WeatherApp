<script setup>
import { reactive } from 'vue'

const emit = defineEmits(['place-data'])

const search = reactive({
  qery: '',
  temeout: null,
  result: null
})

const handleSearch = () => {
  clearTimeout(search.temeout)
  search.temeout = setTimeout(async () => {
    if (search.qery !== '') {
      const response = await fetch(
        `http://api.weatherapi.com/v1/search.json?key=0aa28249b505408c821173040242107&q=${search.qery}`
      )

      const data = await response.json()
      search.result = data
    } else {
      search.result = null
    }
  }, 500)
}

const getWether = async (id) => {
  const response = await fetch(
    `http://api.weatherapi.com/v1/forecast.json?key=0aa28249b505408c821173040242107&q=id:${id}&days=3&aqi=no&alerts=no`
  )

  const data = await response.json()

  emit('place-data', data)

  search.qery = ''

  search.result = null
}
</script>

<template>
  <div>
    <!-- search -->
    <form>
      <div class="bg-white border border-indigo-600/30 rounded-lg shadow-lg flex items-center">
        <i class="fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
        <input
          type="text"
          placeholder="Keresés"
          class="rounded-r-lg p-2 border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset w-full"
          v-model="search.qery"
          @input="handleSearch()"
        />
      </div>
    </form>
    <!-- suggestions -->
    <div class="bg-white my-2 rounded-lg shadow-lg">
      <div v-if="search.result !== null">
        <div v-for="place in search.result" :key="place.id">
          <button
            @click="getWether(place.id)"
            class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left"
          >
            {{ place.name }}, {{ place.region }}, {{ place.country }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
