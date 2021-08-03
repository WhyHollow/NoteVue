<template>
  <div class="container">
    <div class="input_note">
      <input v-model="title" type="text" @keyup.enter="addNote()" />
    </div>
    <div class="notes_wrap">
      <div v-for="(note, i) in noteArr" :key="i">
        <div class="notes_item">
          <h3>{{ note.title }}</h3>
          <input
            type="checkbox"
            :id="i"
            v-model="note.checkedCategories"
            @change="checkNote(i)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Notes',
    data() {
      return {
        title: null,
        noteArr: [],
      };
    },
    methods: {
      addNote() {
        if (!this.title) return;
        this.noteArr.push({ title: this.title });
        this.title = '';
        this.saveTitle();
      },
      checkNote(i) {
        this.noteArr.splice(i, 1);
        this.saveTitle();
      },
      saveTitle() {
        let parsed = JSON.stringify(this.noteArr);
        localStorage.setItem('notes', parsed);
      },
    },
    mounted() {
      if (localStorage.getItem('notes')) {
        try {
          this.noteArr = JSON.parse(localStorage.getItem('notes'));
        } catch (e) {
          localStorage.removeItem('notes');
        }
      }
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container {
    width: 1100px;
    margin: 0 auto;
  }
  .input_note input {
    width: 200px;
  }
  .notes_wrap {
    display: flex;
    align-items: center;
    flex-direction: column;
  }
  .notes_item {
    width: 200px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid #2c3e50;
    padding: 5px;
    margin: 10px 0;
  }
  .notes_item h3 {
    max-width: 80%;
  }
  .notes_item input {
    max-width: 20%;
  }
</style>
