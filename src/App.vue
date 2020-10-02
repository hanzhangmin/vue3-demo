<template>
<div id="app">
  {{message}}
  <button>
    <router-link to="/"> 首页</router-link>
  </button>
  <button>
    <router-link to="/about"> 我的</router-link>
  </button>

  <router-view v-slot="{ Component }">
    <keep-alive>
      <component :is="Component" />
    </keep-alive>
  </router-view>

  <List :list="books" @addlist="addlist"></List>
</div>
</template>

<style lang="scss">
</style>

<script>
// compositionApi
import {
  reactive,
  toRefs,
  watch,
  computed,
  ref
} from "vue"
import {
  useRoute,
  useRouter
} from "vue-router"
import {
  useStore
} from "vuex"

import List from './components/List'
export default {
  components: {
    List
  },
  // 里面没有this ,默认只执行一次

  // props父组件传递的属性 , context 里面有三个方法 attrs:emit:slots
  setup(props, context) {
    const route = useRoute();
    const state = reactive({
      message: "hzm",
      books: ["红楼梦", "水浒传", "三国演义", "西游记"]
    })
    watch(route, (newvalue) => {
      // console.log(route, newvalue);
    })
    const addlist = (book) => {
      state.books.push(book);
    }
    return {
      ...toRefs(state), //   toRefs 将代理封装 ,以实现响应式，还有解构赋值的功能
      addlist
    }
  }
}
</script>
