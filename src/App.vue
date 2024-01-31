<template>
  <div>
    <h1>{{ title }}</h1>
    <div class="message" v-if="message">
      <p>{{ message }}</p>
    </div>
    <!-- //new-note -->
    <div class="new-note">
      <input v-model="note.title" type="text" placeholder="введите заметку" />
      <textarea v-model="note.descr" placeholder="введите описание"></textarea>
      <button @click="addNote">Новая заметка</button>
    </div>

    <!-- //note-list -->
    <div class="notes">
      <div class="note" v-for="(note, index) in notes" :key="index">
        <div class="note-header">
          <p>{{ note.title }}</p>
        </div>
        <div class="note-body">
          <p>{{ note.descr }}</p>
          <span>{{ formatRussianDate(note.date) }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
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
    addNote() {
      let { title, descr } = this.note;
      if (title === "") {
        this.message = "Введите название заметки";
        return false;
      }
      this.notes.push({
        title,
        descr,
        date: new Date(),
      });
      this.message = null;
      this.note.title = "";
      this.note.descr = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
