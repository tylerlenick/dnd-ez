<template>
    <form class="justify-center	w-3/12">
        <label for="default-search"
            class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-gray-300">Search</label>
        <div class="relative">
            <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
                <svg class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="none" stroke="currentColor"
                    viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                </svg>
            </div>
            <input v-model="queryString" type="search" id="default-search"
                class="block p-4 pl-10 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Search Conditions, Spells..." required="">
        </div>
        <div v-if="typeof(res.results) === 'undefined'">Nothing found, type something else...</div>
        <button v-for="(item, key, index) in res.results" @click="showModal=true" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 my-4 border border-blue-700 rounded">
            {{ item.name }}
        </button>
    </form>
    <LazyInfoModal v-if="showModal"/>
</template>

<script setup>
    let showModal = ref(false)
    let queryString = ref('')
    let { data: res } = await useFetch(() => `https://www.dnd5eapi.co/api/${queryString.value}`, { pick: ['results'] } )
    
</script>