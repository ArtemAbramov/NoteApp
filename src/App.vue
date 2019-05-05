<template>
  <div @click='editClose' class="wrapper">
    <div class='wrapper-content'>
      <section>
        <div class="container">
          <div class="app-header">
            <h1> {{ title }} </h1>
          </div>

          <!-- Message -->
          <message v-if='message' :message='message' />

          <!-- NewNote -->
          <newNote :note='note' :priorities='priorities' @addNote='addNote' />

          <!-- Title -->
          <div @click='editClose' class="note-header" style='margin: 56px 0 36px 0;'>
            <h2> {{ title }} </h2>

            <search 
              :value='search' 
              placeholder='Find your note' 
              @search='search = $event' />

            <div class="icons">
              <svg :class='{ active: grid }' @click='grid = true' style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class='{ active: !grid }' @click='grid = false' style="cursor: pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

          <!-- Notes List -->
          <notes :notes='notesFilter' :grid='grid' @remove='removeNote' @editTitle='editTitle' @editDescr='editDescr' @editClose='editClose' />
          
        </div>
      </section>      
    </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'
export default {
  components: {
    message,
    newNote,
    notes,
    search
  },
  data () {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
      priorities: [
        'Standart',
        'Important',
        'Most important'
      ],
      note: {
        title: '',
        descr: '',
        priority: 'Standart',
        titleEdit: false,
        descrEdit: false,
        titleEditText: '',
        descrEditText: ''
      },
      notes: [
        {
          title: 'First Note',
          descr: 'Decription for first note',
          priority: 'Standart',
          titleEdit: false,
          descrEdit: false,
          titleEditText: '',
          descrEditText: '',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Second Note',
          descr: 'Decription for second note',
          priority: 'Standart',
          titleEdit: false,
          descrEdit: false,
          titleEditText: '',
          descrEditText: '',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Third Note',
          descr: 'Decription for third note',
          priority: 'Standart',
          titleEdit: false,
          descrEdit: false,
          titleEditText: '',
          descrEditText: '',
          date: new Date(Date.now()).toLocaleString()
        }
      ]
    }
  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search
      if (!search) return array
      search = search.trim().toLowerCase()
      array =  array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      return array
    }
  },
  methods: {
    addNote () {
      // console.log(this.note)
      let {title, descr, priority, titleEdit, descrEdit, titleEditText, descrEditText} = this.note

      if (title === '') {
        this.message = "Title can't be blank!"
        return false
      }

      this.notes.push({
        title,
        descr,
        priority,
        titleEdit,
        descrEdit,
        titleEditText,
        descrEditText,
        date: new Date(Date.now()).toLocaleString()
      })
      this.note.title = ''
      this.note.descr = ''
      this.note.priority = 'Standart'
      this.message = null
    },
    removeNote (index) {
      this.notes.splice(index, 1)
    },
    editTitle (index) {
      for (let i = 0; i < this.notes.length; i++){
        if (i !== index) {
          this.notes[i].titleEdit = false
          this.notes[i].titleEditText = ''
        }
      }
      this.notes[index].titleEditText = this.notes[index].title
      this.notes[index].titleEdit = true
    },
    editDescr (index) {
      for (let i = 0; i < this.notes.length; i++){
        if (i !== index) {
          this.notes[i].descrEdit = false
          this.notes[i].descrEditText = ''
        }
      }
      this.notes[index].descrEditText = this.notes[index].descr
      this.notes[index].descrEdit = true
    },
    editClose () {
      for (let i = 0; this.notes.length; i++) {
        this.notes[i].titleEdit = false
        this.notes[i].titleEditText = ''
        this.notes[i].descrEdit = false
        this.notes[i].descrEditText = ''
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.app-header {
  text-align: center;

  h1 {
    font-size: 26px;
    color: #402caf;
  }
}
</style>

