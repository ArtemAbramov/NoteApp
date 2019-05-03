<template>
  <div class="notes">
    <div 
      class="note" 
      :class='{ full: !grid, standart: note.priority === "Standart", important: note.priority === "Important", "most-important": note.priority === "Most important" }' 
      v-for="(note, index) in notes" 
      :key="index"
    >
      <div class="note-header" :class="{ full: !grid }">
        <p>{{ note.title }}</p>
        <p style="cursor: pointer;" @click="removeNote(index)">x</p>
      </div>
      <div class="note-body">
        <p>{{ note.descr }}</p>
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
  }
}

.note-header {
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
  p {
    margin: 20px 0;
  }

  span {
    font-size: 14px;
    color: #999;
  }
}
</style>


