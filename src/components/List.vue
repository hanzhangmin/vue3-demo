<template>
<div>
  <ul>
    <li v-for="(li,index) in list" :key="index+'li'">{{li}}</li>
  </ul>
  <input v-model="book" type="text" />
  <button @click="transfer(book)">add</button>
</div>
</template>

<script>
import {
  toRefs,
  reactive
} from 'vue'
export default {
  name: "my-list",
  props: {
    list: Array
  },
  setup(props, contect) {
    // console.log(props.list);
    const state = reactive({
      book: "汉书"
    })
    const transfer = (book) => {
      contect.emit('addlist', book);
    }
    return {
      ...toRefs(state),
      transfer
    }
  }

}
</script>
