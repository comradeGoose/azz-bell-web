<template>
    <form @submit.prevent="onSubmit">
        <button class="btn_add_call" type="submit"><h1>+</h1></button>
    </form>
</template>

<script>
// import LessonCall from '@/components/Lesson/LessonCall.vue'
export default {
  data () {
    return {
    }
  },
  methods: {
    onSubmit () {
      const newLessonCall = {
        id: Date.now(),
        play: false,
        music_name: '',
        week_days: [],
        time_start: '',
        time_end: ''
      }
      this.$emit('Add-LessonCall', newLessonCall)
    }
  }
}
</script>

<style scoped>
div {
    margin: 1em;
}

.btn_add_call {
  width: 50px;
  height: 50px;
  border-radius: 1rem;
  border-color: #2896ea;
  background-color: #2896ea;
  margin: 0;
  padding: 0;
}
h1 {
  margin: 0;
}
</style>
