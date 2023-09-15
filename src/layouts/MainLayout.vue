<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <div class="q-pa-md">
        <h1 class="q-mb-md text-h6 text-center">Star Wars API</h1>
        <q-select
          v-model="selectedEntity"
          :options="entityOptions"
          label="Selecione uma entidade"
          outlined
          emit-value
          map-options
        />
        <q-btn label="Buscar" @click="fetchData" color="primary" class="q-ml-md" />
        <div class="q-mt-md" id="result">
          <q-table :rows="results"
                   :columns="columns"
                   row-key="name" />
        </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  data() {
    return {
      selectedEntity: "films", 
      entityOptions: [
        { label: "Filmes", value: "films" },
        { label: "Pessoas", value: "people" },
        { label: "Planetas", value: "planets" },
        { label: "Espécies", value: "species" },
        { label: "Naves Espaciais", value: "starships" },
        { label: "Veículos", value: "vehicles" },
      ],
      results: [],
      columns: [],
    };
  },
  methods: {
    fetchData() {
      fetch(`https://swapi.dev/api/${this.selectedEntity}/`)
        .then(response => response.json())
        .then(data => {
          this.results = data.results;
          this.columns = Object.keys(this.results[0]).map(header => ({
            name: header,
            required: true,
            label: header,
            align: "left",
            field: header,
          }));
        });
    },
  },
};
</script>
