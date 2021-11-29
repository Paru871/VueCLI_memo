<template>
  <section class="container-fluid bg-light border">
    <h1 class="mt-2">MY MEMOS</h1>
    <div v-for="(memo, key) in memos" :key="memo">
      <ul class="list-group">
        <li class="list-group-item">
          <a href="#" @click="editMemo(memo, key)">{{memo.split("\n")[0]}}</a>
        </li>
      </ul>
    </div>
    <button class="btn btn-outline-success btn-sm mt-2 mb-2 font-weight-bold" @click="showAddForm">+</button>

    <div v-if="showFormToggle">
      <h4>{{ formTitle }}</h4>
      <div v-if="formMode === 'add'">
        <textarea rows="10" cols="55" v-model="newMemo"></textarea>
        <button class="btn btn-outline-primary btn-sm mb-2" @click="addMemo">Save</button>
        <button class="btn btn-outline-warning btn-sm ms-2 mb-2" @click="addCancel">Cancel</button>
      </div>
      <div v-else-if="formMode === 'edit'">
        <textarea rows="10" cols="55" v-model="renewedMemo"></textarea>
        <button class="btn btn-outline-info btn-sm mb-2" @click="updateMemo(editKey)">Update</button>
        <button class="btn btn-sm btn-outline-danger ms-2 mb-2" @click="removeMemo(editKey)"
        >Delete</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data () {
    return {
      memos: [],
      newMemo: null,
      renewedMemo: null,
      editKey: null,
      showFormToggle: false,
      formMode: null
    }
  },
  mounted () {
    if (localStorage.getItem('memos')) {
      this.memos = JSON.parse(localStorage.getItem('memos'))
    }
  },
  methods: {
    showAddForm () {
      this.showFormToggle = true
      this.formTitle = 'Add Memo'
      this.formMode = 'add'
    },
    addMemo () {
      if (this.newMemo) {
        this.memos.push(this.newMemo)
        this.newMemo = ''
        this.saveMemos()
      }
    },
    addCancel () {
      this.newMemo = ''
      this.showFormToggle = false
    },
    editMemo (memo, key) {
      this.showFormToggle = true
      this.formTitle = 'Edit/Delete Memo'
      this.formMode = 'edit'
      this.editKey = key
      this.renewedMemo = memo
    },
    removeMemo (key) {
      this.memos.splice(key, 1)
      this.saveMemos()
    },
    updateMemo (key) {
      console.log(key)
      this.memos[key] = this.renewedMemo
      this.saveMemos()
      this.renewedMemo = ''
      this.editKey = ''
    },
    saveMemos () {
      const parsed = JSON.stringify(this.memos)
      localStorage.setItem('memos', parsed)
      this.showFormToggle = false
    }
  }
}
</script>

<style>
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  max-width: 500px;
}
.font-weight-bold {
  font-weight: 700 !important;
}
.btn {
    border-radius: 6px;
}
.list-group-item {
    font-family: "Open Sans", "Helvetica Neue", Helvetica, Arial, "游ゴシック体", "Yu Gothic", YuGothic, "Hiragino Kaku Gothic ProN", Meiryo, sans-serif
}
h1 {
    font-family: var(--font-family-sans-serif);
}

</style>
