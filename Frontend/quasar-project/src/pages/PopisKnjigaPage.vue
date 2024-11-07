<template>
  <div class="popis-knjiga-page">
    <q-table
      :rows="books"
      :columns="columns"
      row-key="id"
      :pagination="pagination"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const columns = [
  {
    name: 'id',
    label: 'ID',
    align: 'left',
    field: row => row.id,
    sortable: true
  },
  {
    name: 'title',
    label: 'Naziv',
    align: 'left',
    field: row => row.title,
    sortable: true
  },
  {
    name: 'author',
    label: 'Autor',
    align: 'left',
    field: row => row.author,
    sortable: true
  },
  {
    name: 'year',
    label: 'Godina izdanja',
    align: 'left',
    field: row => row.year,
    sortable: true
  }
];

const books = ref([
  { id: 1, title: 'A Court of Thorns and Roses', author: 'Sarah J. Maas', year: 2021 },
  { id: 2, title: 'A Court of Mist and Fury', author: 'Sarah J. Maas', year: 2020 },
  { id: 3, title: 'Never Lie', author: 'Freida McFadden', year: 2019 },
  { id: 4, title: 'It Ends With Us', author: 'Coleen Hoover', year: 2022 }
]);

const pagination = ref({
  page: 1,
  rowsPerPage: 5
});
</script>

<style scoped>
.popis-knjiga-page {
  padding: 20px;
}
</style>

