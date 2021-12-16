<script setup>
const id = useState('id', () => 13);
const loading = useState('loading', () => false);
const contents = useState('contents', () => null);

async function fetchData() {
  try {
    loading.value = true;
    const { data } = await useFetch(`https://www.swapi.tech/api/people/${id.value}`); // prettier-ignore
    if (!data) throw new Error('cannot fetch data');
    contents.value = data;
  } catch (error) {
    console.error(error.message);
    contents.value = null;
  } finally {
    loading.value = false;
  }
}
</script>

<template>
  <div class="space-y-4">
    <div>
      <h1 class="text-2xl font-bold">Get your Star Wars data</h1>
    </div>

    <div>
      <label class="block font-bold">Choose Character ID</label>
      <div class="mt-2 space-x-4">
        <input
          @keyup.enter="fetchData"
          v-model="id"
          class="
            py-2
            px-4
            border border-gray-300
            focus:border-green-600
            rounded
            focus:outline-none
          "
        />
        <button
          @click="fetchData"
          class="py-2 px-4 bg-green-500 hover:bg-green-600 text-white rounded"
        >
          {{ loading ? 'Loading ...' : 'Fetch Data' }}
        </button>
      </div>
    </div>

    <template v-if="!loading && contents">
      <div>
        <pre class="bg-slate-100 text-sm rounded text-gray-800">
          <code>
            {{ contents }}
          </code>
        </pre>
      </div>
    </template>
  </div>
</template>
