<template>
  <div>{{ msg }}</div>
  <div v-for="thread in sourceData.threads" :key="thread.id">
    <h2>{{ thread.title }}</h2>
    <div v-for="postId in thread.posts" :key="postId">
        <p><b>{{ findObjectDataById("users", findObjectDataById("posts", postId).userId).name }}</b></p>
        <p>{{ findObjectDataById("posts", postId).text }}</p>
    </div>
  </div>
</template>

<script>
import sourceData from '@/data.json'

export default {
  props: {
    msg: {
      type: String,
      default: 'Hello!'
    }
  },
  data () {
    return {
      threads: sourceData.threads,
      sourceData: sourceData
    }
  },
  methods: {
    findObjectDataById (prop, id) {
      if (!(prop in this.sourceData)) return null

      return this.sourceData[prop].find(d => d.id === id)
    }
  }
}
</script>

<style>

</style>
