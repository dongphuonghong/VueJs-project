<template>
  <div class="hello">
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap...in.css">
      <h1>Bài 2</h1>
      <div class="container text-center">
          <div class="row">
              <div class="col">
                  <button type="button" class="btn btn-success" @click="addNote()">+ Add Note</button>
                  <div id="nameNote" v-for="(note, index) in notes" :key="index" class="d-flex justify-content-around"
                      @click="selectNote(note)">
                      <p style="margin: 0;">{{ note.name }}</p>
                      <button type="button" class="btn btn-sm ml-2" @click="toggleFavorite(note)">
                          <i :class="[note.favorite ? 'bi bi-star-fill' : 'bi bi-star']"></i>
                      </button>
                  </div>
              </div>
              <div class="col text-start">
                  <div class="d-flex">
                      <input v-model="newNote.name" style="width: 300px;" type="text" class="form-control"
                          placeholder="Enter note name">
                      <button type="button" class="btn btn-sm btn-primary ml-2" @click="toggleFavorite(newNote)">
                          <i :class="[newNote.favorite ? 'bi bi-star-fill' : 'bi bi-star']"></i>
                      </button>
                      <button type="button" class="btn btn-success" @click="deleteNote()"><i
                              class="bi bi-trash3-fill"></i></button>
                  </div>
                  <textarea v-model="newNote.content" name="" id="" cols="30" rows="10"></textarea>
              </div>
              <div class="col">
                  <div v-if="selectedNote">
                      <p>{{ selectedNote.content }}</p>
                  </div>
              </div>
          </div>
          <div class="row">
              <div class="col">

              </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
      return {
          notes: [], // Danh sách ghi chú
          newNote: { name: '', content: '', favorite: false }, // Biến để lưu trữ ghi chú mới
          selectedNote: null // Biến để lưu trữ ghi chú đang được chọn
      }
  },
  methods: {
      addNote() {
          if (this.newNote.name.trim() !== '' && this.newNote.content.trim() !== '') {
              this.notes.push({ ...this.newNote });
              this.newNote.name = ''; // Xóa nội dung trường nhập sau khi thêm ghi chú
              this.newNote.content = ''; // Xóa nội dung trường nhập sau khi thêm ghi chú
          }
      },
      toggleFavorite(note) {
          note.favorite = !note.favorite;
      },
      deleteNote() {
          // Xóa ghi chú đang được chọn
if (this.selectedNote) {
              const index = this.notes.indexOf(this.selectedNote);
              if (index !== -1) {
                  this.notes.splice(index, 1);
                  this.selectedNote = null; // Đặt lại ghi chú đang được chọn sau khi xóa
              }
          }
      },
      selectNote(note) {
          // Chọn ghi chú để hiển thị nội dung
          this.selectedNote = note;
      }
  }
}
</script>

<style scoped>
#nameNote {
  cursor: pointer;
  display: flex;
  align-items: center;
}


#nameNote:hover {
  background-color: #16a34a;
  color: white;
}
</style>