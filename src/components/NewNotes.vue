<template>
  <div class="new-note">
    <label for="">Название</label>
    <input
      v-model="localNote.title"
      type="text"
      placeholder="Введите название заметки"
    />
    <label for="">Описание</label>
    <textarea
      v-model="localNote.descr"
      placeholder="Введите описание"
    ></textarea>
    <button class="btn btnPrimary addNote" @click="emitAddNote">
      Добавить заметку
    </button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      localNote: {
        title: this.note.title,
        descr: this.note.descr,
      },
    };
  },
  methods: {
    emitAddNote() {
      this.$emit("addNote", { ...this.localNote });
      this.localNote.title = "";
      this.localNote.descr = "";
    },
  },
};
</script>

<style lang="scss" scoped>
.new-note {
  text-align: center;
}
.addNote {
  margin-top: 30px;
  margin-bottom: 30px;
}
</style>
