<template>
  <div class="home">
    
    <div>
      <div>
        <input type="text" 
        class="note-input" 
        placeholder="type the name of your note"
        v-model="newNoteName">
      </div>
      <div>
        <textarea type="text" 
                class="note-input-content" 
                placeholder="type in your note brother"
                v-model="newNoteContent"></textarea>
      </div>
        
        <button v-on:click="submit">Submit</button>

    </div>
    

    



    <!-- notes list -->
    <div v-for="note in notes" :key="note.id">
      <div v-if="!note.editing">
        <div
        class="notes-list-div">
          <h1>{{ note.title }}</h1>
          <div class="remove-note" @click="removeNote(note)">
            &times;
          </div>
        </div>
        <div>
        <p>{{ note.content }}</p>
      </div>
      </div>
      <div v-else>
      <div>
            <input 
              class="edit-note"
              type="text"
              v-model="note.title">
            </div>
          
          <div>
              <input
              class="edit-note"
              type="text"
              v-model="note.content">
          </div>
          <div class="done-edit" @click="doneEdit(note)">
            <p>submit</p>
          </div>
        
        </div>
      
      
      
      <div class="comment">
        <div class="edit-note" @click="edit(note)">
          <p>edit</p>
        </div>
        <router-link v-bind:to="'/note/' + note.id">comments</router-link>
      </div>
    </div>




    
    
  </div>
</template>

<script>
// @ is an alias to /src
import { db } from '../db'

export default {
  name: "notes-list",
  data(){ 
    return {
    newNoteName: '',
    newNoteContent: '',
    notes: [],
// title: 
// editing:
// submitted
    }
  },
  
  methods: {
    submit(){
      if (this.newNoteName.length === 0 || this.newNoteContent.length === 0) {
        return 
      } else {
      db.collection('notes').add({
      title: this.newNoteName,
      content: this.newNoteContent,
      editing: false
  })
    this.newNoteName = '',
    this.newNoteContent = ''

    }
    },
    removeNote(note) {
      db.collection('notes').doc(note.id).delete()
    },
    edit(note){
      db.collection('notes').doc(note.id).update({ editing: true })
      
    },
    doneEdit(note){
      if (note.title.length === 0 && note.content.length === 0) {
        this.removeNote(note)
      } else {
      db.collection('notes').doc(note.id).update({ title: note.title, content: note.content, editing: false })
      }
    }
  },
  firestore: {
    notes: db.collection('notes'),
  },
}
</script>

<style lang="scss">

.home{
  margin: 0 auto;
  width: 75%
}

.note-input {
  width: 75%;
  font-size: 16px;
  margin-bottom: 16px;
  padding: 5px;
  &:focus {
      outline: 0;
    }
  border: 1px solid gray;
}

.notes-list-div {
  display: flex;
  margin-right:10px;
  align-items: center;
  justify-content: space-between;
  width: 75%;
  
  
}

.comment p {
  text-align: right;
  width: 75%;
  color: rgb(0, 195, 255);
  margin-right: 10px
}

.comment {
  display: flex;
  justify-content: flex-end;
  width: 75%;
}

button {
  margin-bottom: 20px;
  margin-top: 5px;
  background-color: transparent;
  border: 1px solid gray;
}

textarea {
  width: 75%;
  &:focus {
      outline: 0;
    }
  padding: 5px;
}

.remove-note {
        cursor: pointer;
        margin-left: 14px;
        &:hover {
            color:red;
        }
    }

  .edit-note p {
    cursor: pointer;
        margin-right: 10px;
        &:hover {
            color:purple;
        }
  }

  input {
    margin-bottom: 10px;
  }

  .done-edit p {
    cursor: pointer;
        margin-right: 10px;
        &:hover {
            color:purple;
        }
  }
</style>