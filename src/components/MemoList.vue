<template>
<div class="list-group">
  <a href="#" class="list-group-item list-group-item-action" v-for="(memo, index) in memos" :key="memo.id" @click.prevent="$emit('show', index)">{{ memo.content.split('\n')[0] }}</a>
  <a href="" class="list-group-item list-group-item-action" @click.prevent="$emit('add')">+</a>
</div>
</template>

<script>
export default {
  name: 'MemoList',
  props: {
    memos: Array
  }
}
</script>
