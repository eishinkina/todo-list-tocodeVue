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
    <div>
      <select v-model="localNote.type">
        <option value="1">Обычная</option>
        <option value="2">Важная</option>
        <option value="3">Очень важная</option>
      </select>
    </div>
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
        type: this.note.type,
      },
    };
  },
  methods: {
    emitAddNote() {
      this.$emit("addNote", { ...this.localNote });
      this.localNote.title = "";
      this.localNote.descr = "";
      this.localNote.type = "1";
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

select {
  margin-top: 30px;
  background-color: white;
  border: 1px solid lightgray;
  padding: 16px;
  font-size: 16px;
  border-radius: 30px;
  width: 400px;
  color: gray;
}
</style>
