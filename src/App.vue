<template>
  <div>
    <button v-on:click="addNewNote" class="new-button">Take a new note</button>
    <div class="notes-area">
      <ul class="notes">
        <li v-for="(note, index) in notes" :key="note.id" class="note">
          <p class="title">{{ note.title }}</p>
          <button v-on:click="setEditInfo(index)" class="show-button">
            Show
          </button>
          <button v-on:click="removeNote(index)" class="delete-button">
            Delete
          </button>
        </li>
      </ul>
    </div>
    <Note
      v-if="isEdittable()"
      :focusedId="editIndex"
      :content="notes[editIndex].content || ''"
      :title="notes[editIndex].title || ''"
      :paramTitle="temporaryTitle"
      :paramContent="temporaryContent"
      v-on:update:paramTitle="updateTitle"
      v-on:update:paramContent="updateContent"
      v-on:editnote="editNote"
    ></Note>
    <button
      v-if="isEdittable()"
      v-on:click="finishEdit()"
      class="button-footer"
    >
      Finish
    </button>
    <button
      v-if="isEdittable()"
      v-on:click="removeNote(editIndex)"
      class="button-footer"
    >
      Delete
    </button>
  </div>
</template>

<script>
import Note from './components/Note.vue';
export default {
  name: 'App',
  components: {
    Note,
  },
  data() {
    return {
      targetNoteContent: '',
      targetNoteTitle: '',
      editIndex: -1,
      notes: [],
    };
  },
  mounted() {
    this.notes = JSON.parse(localStorage.getItem('access_notes')) || [];
  },
  computed: {},
  methods: {
    addNewNote() {
      this.editIndex = this.notes.length;
      this.temporaryTitle = '';
      this.temporaryContent = '';
      this.notes.push({
        id: this.setNextNoteId(),
        title: '',
        content: '',
      });
      this.saveNotes();
    },
    setNextNoteId() {
      if (this.notes.length == 0) return 0;
      const ids = this.notes.map((x) => x.id);
      return Math.max(...ids) + 1;
    },
    editNote() {
      this.notes.splice(this.editIndex, 1, {
        id: this.notes[this.editIndex].id,
        title: this.temporaryTitle,
        content: this.temporaryContent,
      });
      this.saveNotes();
    },
    setEditInfo(index) {
      this.temporaryTitle = this.notes[index].title;
      this.temporaryContent = this.notes[index].content;
      this.editIndex = index;
      this.targetNoteTitle = this.notes[index].title;
      this.targetNoteContent = this.notes[index].content;
    },
    removeNote(index) {
      this.notes.splice(index, 1);
      this.saveNotes();
      this.editIndex = -1;
    },
    saveNotes() {
      localStorage.setItem('access_notes', JSON.stringify(this.notes));
    },
    isEdittable() {
      const notEdittable = -1;
      return this.editIndex != notEdittable;
    },
    finishEdit() {
      const notEdittable = -1;
      return (this.editIndex = notEdittable);
    },
    updateTitle(title) {
      this.temporaryTitle = title;
      this.editNote();
    },
    updateContent(content) {
      this.temporaryContent = content;
      this.editNote();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: '游ゴシック体', 'YuGothic', '游ゴシック', 'Yu Gothic',
    'ヒラギノ角ゴ Pro W3', 'Hiragino Kaku Gothic Pro', 'メイリオ', 'Meiryo',
    sans-serif;
}
.notes-area {
  height: 300px;
  width: 60%;
  margin-left: auto;
  margin-right: auto;
  margin-top: 15px;
  margin-bottom: 10px;
  overflow-y: scroll;
}
.note {
  display: flex;
  justify-content: center;
  align-items: center;
}
.title {
  font-size: 15px;
  width: 40%;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
button {
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 10px;
  padding-right: 10px;
  font-size: 15px;
  border-radius: 3px;
  background: #383838;
  color: #fff;
  border: none;
  position: relative;
  cursor: pointer;
  transition: 800ms ease all;
  outline: none;
}
/* かっこいいボタンデザイン(コピー) */
button:hover {
  background: #fff;
  color: #383838;
}
button:before,
button:after {
  content: '';
  position: absolute;
  top: 0;
  right: 0;
  height: 2px;
  width: 0;
  background: #383838;
  transition: 400ms ease all;
}
button:after {
  right: inherit;
  top: inherit;
  left: 0;
  bottom: 0;
}
button:hover:before,
button:hover:after {
  width: 100%;
  transition: 800ms ease all;
}
/* かっこいいボタンデザイン終わり */
button.show-button {
  margin-left: 10px;
  margin-right: 10px;
}

button.button-footer {
  display: block;
  margin-top: 15px;
  margin-left: auto;
  margin-right: auto;
}
</style>
