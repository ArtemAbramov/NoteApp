<template>
  <div class="notes">
    <div 
      class="note" 
      :class='{ full: !grid, standart: note.priority === "Standart", important: note.priority === "Important", "most-important": note.priority === "Most important" }' 
      v-for="(note, index) in notes" 
      :key="index"
      @click.stop = ''
    >
      <div class="note-header" :class="{ full: !grid }">
        <p v-if='!note.titleEdit' @click='$emit("editTitle",index)'>{{ note.title }}</p>
        <input 
          v-model = 'note.titleEditText' 
          v-if="note.titleEdit" 
          type="text" 
          @keyup.enter = 'note.title = note.titleEditText, note.titleEdit = false, note.titleEditText = ""'
        >
        <p style="cursor: pointer;" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p v-if='!note.descrEdit' @click='$emit("editDescr",index)'>{{ note.descr }}</p>
        <input 
          v-model = 'note.descrEditText' 
          v-if="note.descrEdit" 
          type="text"
          @keyup.enter = 'note.descr = note.descrEditText, note.descrEdit = false, note.descrEditText = ""'
        >
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: {
      type: Array,
      required: true
    },
    grid: {
      type: Boolean,
      required: true
    }
  },
  mounted () {
    document.body.addEventListener('keyup', e => {
      if (e.keyCode === 27) {
        this.$emit('editClose')
      }
    })
  },
  methods: {
    removeNote(index) {
      this.$emit("remove", index);
    }
  }
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
  transition: all .25s cubic-bezier(.02,.01,.47,1);
  box-shadow: 0 10px 10px rgba(0,0,0,.5);

  .note-header {
    input {
      margin-bottom: 0;
      width: 80%;
      height: 40px;
      color: #402caf;
      font-size: 22px;
    }
  }

  .note-body {
    input {
      margin: 20px 0;
      width: 90%;
      height: 40px;
    }
  }

  &.standart {
    box-shadow: 0 10px 10px rgba(#43A047,.5);
  }

  &.important {
    box-shadow: 0 10px 10px rgba(#FDD835,.5);
  }

  &.most-important {
    box-shadow: 0 10px 10px rgba(#DD2C00,.5);
  }

  &:hover {
    box-shadow: 0 10px 10px rgba(0,0,0,1);
    transform: translate(0,-6px);
    transition-delay: 0s !important;

    &.standart {
      box-shadow: 0 10px 10px rgba(#43A047,1);
    }

    &.important {
      box-shadow: 0 10px 10px rgba(#FDD835,1);
    }

    &.most-important {
      box-shadow: 0 10px 10px rgba(#DD2C00,1);
    }
  }

  &.full {
    width: 100%;
    text-align: center;

    .note-header {
      input {
        margin-right: 20px;
        width: 50%;
        text-align: center;
      }
    }

    .note-body {
      display: flex;
      align-items: center;
      flex-direction: column;
      input {
        width: 60%;
        text-align: center;
      }
    }
  }
}

.note-header {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;

  h2 {
    font-size: 32px;
  }

  &.full {
    justify-content: center;

    p {
      margin-right: 16px;

      &:last-child {
        margin-right: 0;
      }
    }
  }

  p {
    color: #402caf;
    font-size: 22px;
  }
  svg {
    margin-right: 12px;
    color: #999;

    &.active {
      color: #402caf;
    }

    &:last-child {
      margin-right: 0;
    }
  }
}

.note-body {
  position: relative;

  p {
    margin: 20px 0;
  }

  span {
    font-size: 14px;
    color: #999;
  }
}
</style>


