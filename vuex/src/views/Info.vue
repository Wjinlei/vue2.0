<template>
  <div>
  This is Info Page
  <button type="button" @click="add()">添加count</button>
  </div>
</template>

<script>
import store from '@/store'
export default {
    name: "Info",
    store,
    methods: {
        add() {
            store.commit("plus")
        }
    }
}
</script>

<style>

</style>
