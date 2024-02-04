<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <MessageBar v-if="message" :message="message" />
          <NewNotes :note="note" @addNote="addNote" />
          <SearchBar
            :value="search"
            placeholder="Найти вашу заметку"
            @search="search = $event"
          />
          <div class="note-header">
            <h1>{{ title }}</h1>

            <div class="icons">
              <svg
                :class="{ active: grid }"
                @click="grid = true"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="3" y="3" width="7" height="7"></rect>
                <rect x="14" y="3" width="7" height="7"></rect>
                <rect x="14" y="14" width="7" height="7"></rect>
                <rect x="3" y="14" width="7" height="7"></rect>
              </svg>
              <svg
                :class="{ active: !grid }"
                @click="grid = false"
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <line x1="8" y1="6" x2="21" y2="6"></line>
                <line x1="8" y1="12" x2="21" y2="12"></line>
                <line x1="8" y1="18" x2="21" y2="18"></line>
                <line x1="3" y1="6" x2="3" y2="6"></line>
                <line x1="3" y1="12" x2="3" y2="12"></line>
                <line x1="3" y1="18" x2="3" y2="18"></line>
              </svg>
            </div>
          </div>

          <NotesBar
            :notes="notesFiltered"
            :format="formatRussianDate"
            @removeNote="removeNote"
            :grid="grid"
          />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import MessageBar from "./components/MessageBar.vue";
import NewNotes from "./components/NewNotes.vue";
import NotesBar from "./components/NotesBar.vue";
import SearchBar from "./components/SearchBar.vue";
export default {
  components: {
    MessageBar,
    NewNotes,
    NotesBar,
    SearchBar,
  },
  data() {
    return {
      title: "Приложение для заметок",
      message: null,
      grid: true,
      search: "",
      note: {
        title: "",
        descr: "",
        type: "1",
      },
      notes: [
        {
          title: "Первая заметка",
          descr: "Описание первой заметки",
          date: new Date(),
          type: 1,
        },
        {
          title: "Вторая заметка",
          descr: "Описание второй заметки",
          date: new Date(),
          type: 2,
        },
        {
          title: "Третья заметка",
          descr: "Описание третьей заметки",
          date: new Date(),
          type: 3,
        },
      ],
    };
  },
  methods: {
    formatRussianDate(date) {
      return date.toLocaleString("ru-RU", {
        weekday: "short",
        year: "numeric",
        month: "short",
        day: "numeric",
        hour: "2-digit",
        minute: "2-digit",
        second: "2-digit",
      });
    },
    addNote(newNote) {
      if (newNote.title === "") {
        this.message = "Введите название заметки";
        return false;
      }
      this.notes.push({
        ...newNote,
        date: new Date(),
      });
      this.message = null;
    },
    removeNote(index) {
      this.notes = this.notes.filter((note, i) => i !== index);
    },
  },
  computed: {
    notesFiltered() {
      return this.notes.filter((note) => {
        return note.title.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },
};
</script>

<style lang="scss">
h1 {
  font-size: 32px;
  color: #999;
}

.green {
  border: 1px solid green;
}
.red {
  border: 1px solid red;
}
</style>
