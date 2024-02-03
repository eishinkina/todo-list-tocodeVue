<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <h1 class="title">{{ title }}</h1>
          <MessageBar v-if="message" :message="message" />
          <NewNotes :note="note" @addNote="addNote" />
          <!-- //note-list -->
          <NotesBar :notes="notes" :format="formatRussianDate" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import MessageBar from "./components/MessageBar.vue";
import NewNotes from "./components/NewNotes.vue";
import NotesBar from "./components/NotesBar.vue";
export default {
  components: {
    MessageBar,
    NewNotes,
    NotesBar,
  },
  data() {
    return {
      title: "Приложение для заметок",
      message: null,
      note: {
        title: "",
        descr: "",
      },
      notes: [
        {
          title: "Первая заметка",
          descr: "Описание первой заметки",
          date: new Date(),
        },
        {
          title: "Вторая заметка",
          descr: "Описание второй заметки",
          date: new Date(),
        },
        {
          title: "Третья заметка",
          descr: "Описание третьей заметки",
          date: new Date(),
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
  },
};
</script>

<style lang="scss" scoped>
.title {
  text-align: center;
  margin-bottom: 30px;
}
</style>
