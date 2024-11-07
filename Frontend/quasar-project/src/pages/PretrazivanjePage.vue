<template>
  <q-page padding>
    <!-- Pretraga -->
    <div class="q-mb-md">
      <q-input
        v-model="searchQuery"
        label="Unesite pojam za pretragu"
        filled
        class="q-mb-md"
        debounce="300"
      />

      <div class="q-mb-md">
        <q-checkbox
          v-model="searchByAuthor"
          label="Pretražuj po autoru"
        />
        <q-checkbox
          v-model="searchByTitle"
          label="Pretražuj po naslovu"
        />
      </div>

      <q-btn @click="performSearch" label="Traži" color="primary" />

      <!-- Tablica sa rezultatima -->
      <q-table
        :rows="filteredBooks"
        :columns="columns"
        row-key="id"
        class="q-mt-md"
      >
        <template v-slot:body="props">
          <q-tr :props="props">
            <q-td :props="props" prop="title" />
            <q-td :props="props" prop="author" />
          </q-tr>
        </template>
      </q-table>
    </div>
  </q-page>
</template>

<script>
import { ref, computed, watch } from "vue";

export default {
  name: "PretrazivanjePage",
  setup() {
    // Dummy podaci za testiranje
    const books = ref([
      { id: 1, title: 'A Court of Thorns and Roses', author: 'Sarah J. Maas' },
      { id: 2, title: 'A Court of Mist and Fury', author: 'Sarah J. Maas' },
      { id: 3, title: 'Never Lie', author: 'Freida McFadden' },
      { id: 4, title: 'It Ends With Us', author: 'Coleen Hoover' },
    ]);

    // Statička pretraga
    const searchQuery = ref("");
    const searchByAuthor = ref(false);
    const searchByTitle = ref(true);

    // Kolone tablice
    const columns = [
      { name: "title", label: "Naslov", required: true, align: "left", field: "title" },
      { name: "author", label: "Autor", required: true, align: "left", field: "author" }
    ];

    // Funkcija za obavljanje pretrage
    const performSearch = () => {
      console.log("Performing search with query:", searchQuery.value);
      filteredBooks.value = books.value.filter((book) => {
        const searchText = searchQuery.value.toLowerCase();
        let matches = false;

        // Ako je odabrano pretraživanje po naslovu
        if (searchByTitle.value && book.title.toLowerCase().includes(searchText)) {
          matches = true;
        }

        // Ako je odabrano pretraživanje po autoru
        if (searchByAuthor.value && book.author.toLowerCase().includes(searchText)) {
          matches = true;
        }

        return matches;
      });
      console.log("Filtered books:", filteredBooks.value);
    };

    // Reaktivno praćenje promjena unosa u pretragu
    const filteredBooks = ref(books.value);

    // Watch za praćenje promjena unosa i checkboxova
    watch([searchQuery, searchByAuthor, searchByTitle], () => {
      performSearch(); // Automatski pokreće pretragu kad god se promijene ovi podaci
    });

    return {
      searchQuery,
      searchByAuthor,
      searchByTitle,
      columns,
      filteredBooks,
      performSearch,
    };
  },
};
</script>

<style scoped>
/* Stilizacija inputa i tablice */
.q-table {
  min-height: 300px;
}

.q-checkbox {
  margin-right: 20px;
}
</style>
