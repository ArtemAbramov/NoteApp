<template>
  <div class="wrapper">
    <div class='wrapper-content'>
      <section>
        <div class="container">

          <!-- Title -->
          <h1> {{ title }} </h1>

          <!-- Message -->
          <message v-if='message' :message='message' />

          <!-- NewNote -->
          <newNote 
            :note='note' 
            @addNote='addNote' 
          />

          <!-- Notes -->
          <notes 
            :notes='notes'
            @remove='removeNote'
          />
          
        </div>
      </section>      
    </div>
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newNote from '@/components/NewNote.vue'
import notes from '@/components/Notes.vue'
export default {
  components: {
    message,
    newNote,
    notes
  },
  data () {
    return {
      title: 'Notes App',
      message: null,
      note: {
        title: '',
        descr: ''
      },
      notes: [
        {
          title: 'First Note',
          descr: 'Decription for first note',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Second Note',
          descr: 'Decription for second note',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Third Note',
          descr: 'Decription for third note',
          date: new Date(Date.now()).toLocaleString()
        }
      ]
    }
  },
  methods: {
    addNote () {
      // console.log(this.note)
      let {title, descr} = this.note

      if (title === '') {
        this.message = "title can't be blank!"
        return false
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString()
      })
      this.note.title = ''
      this.note.descr = ''
      this.message = null
    },
    removeNote (index) {
      this.notes.splice(index, 1)
    }
  }
}
</script>

<style>
</style>
