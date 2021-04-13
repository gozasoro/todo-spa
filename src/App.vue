<template>
  <div class="container-sm">
    <div class="row">
      <div class="col-sm-6 bg-white mx-auto mt-5 p-3 border rounded row">
        <div class="col-sm-6">
          <MemoList :memos="memos" @show="showMemo($event)" @add="addNewMemo"></MemoList>
        </div>
        <div class="col-sm-6">
          <textarea class="form-control mb-2" rows="5" v-model="editableContent" ref="focusArea"></textarea>
          <div class="d-flex">
            <button @click="editMemo" class="btn btn-success flex-grow-1">編集</button>
            <button @click="deleteMemo" class="btn btn-danger ms-2">削除</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MemoList from './components/MemoList.vue'

export default {
  name: 'App',
  components: {
    MemoList
  },
  data () {
    return {
      editableContent: '',
      editableIndex: null,
      memos: [
        {
          id: 0,
          content: 'sample memo'
        }
      ],
      nextId: 1
    }
  },
  created () {
    const localData = JSON.parse(localStorage.getItem('memos'))
    console.log(localData)
    if (localData && localData.length) {
      this.memos = localData
      this.nextId = localData[this.memos.length - 1].id + 1
    }
  },
  updated () {
    localStorage.setItem('memos', JSON.stringify(this.memos))
  },
  methods: {
    addNewMemo () {
      this.memos.push({
        id: this.nextId,
        content: ''
      })
      this.showMemo(this.memos.length - 1)
      this.$refs.focusArea.focus()
    },
    showMemo (index) {
      this.editableIndex = index
      this.editableContent = this.memos[index].content
    },
    editMemo () {
      if (this.editableIndex === null) return
      this.memos[this.editableIndex].content = this.editableContent
      this.editableIndex = null
      this.editableContent = ''
    },
    deleteMemo () {
      if (this.editableIndex === null) return
      this.memos.splice(this.editableIndex, 1)
      this.editableIndex = null
      this.editableContent = ''
    }
  }
}
</script>
