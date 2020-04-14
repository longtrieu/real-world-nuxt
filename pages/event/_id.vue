<template>
  <div>
    <h1>This is event {{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await $axios.get(
        'http://localhost:3001/events/' + params.id
      )
      return {
        event: data
      }
    } catch (e) {
      error({
        status: 503,
        message: 'Unable to fetch event #' + params.id
      })
    }
  },
  head() {
    return {
      title: this.event.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'What you need to know about event #' + this.event.title
        }
      ]
    }
  }
}
</script>

<style scoped></style>
