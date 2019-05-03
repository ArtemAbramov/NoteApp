<template>
  <!-- new note -->
  <div class="new-note">
    <label>Title</label>
    <input v-model='note.title' type="text">
    <label>Priority</label>
    <select v-model='note.priority'>
      <option v-for='(priority, index) in priorities' :key='index'>
        {{ priority }}
      </option>
    </select>
    <label>Description</label>
    <textarea v-model='note.descr'></textarea>
    <button class="btn btnPrimary" @click='addNote'>New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    },
    priorities: {
      type: Array,
      required: true
    }
  },
  methods: {
    addNote () {
      this.$emit('addNote', this.note)
    }
  }
}
</script>

<style lang="scss">
.new-note {
  margin-top: 20px;
  text-align: center;

  select {
    margin-bottom: 30px;
    padding: 10px 14px;
    border-radius: 20px;
  }

  textarea {
    margin-bottom: 20px;
  }
}
</style>


