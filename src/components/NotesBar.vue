<template>
  <div>
    <div class="notes">
      <div
        class="note"
        v-for="(note, index) in notes"
        :key="index"
        :class="{ full: !grid }"
      >
        <div class="note-header">
          <p>{{ note.title }}</p>
          <p style="cursor: pointer" @click="removeNote(index)">X</p>
        </div>
        <div class="note-body">
          <p>{{ note.descr }}</p>
          <span>{{ format(note.date) }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true,
    },
    format: {
      type: Function,
      required: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      console.log(`Удаление заметки -id: ${index}`);
      this.$emit("removeNote", index);
    },
  },
};
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}

.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #fff;
  transition: all 0.25s cubic-bezier(0.2, 0.1, 0.47, 1);
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.2);
  &:hover {
    box-shadow: 0 30px 30px rgba(0, 0, 0, 0.4);
    transform: translate(0, -6px);
    transition-delay: 0s !important ;
  }
  &.full {
    width: 100%;
  }
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  p {
    color: #0425bb;
    font-size: 22px;
  }
  svg {
    cursor: pointer;
    margin-right: 12px;
    color: #999;
    &.active {
      color: #0425bb;
    }
    &:last-child {
      margin-right: 0;
    }
  }
}
.note-body {
  p {
    margin: 20px 0;
  }
  span {
    font-size: 14px;
    color: #999;
  }
}
</style>
