<template>
    <ul>
      <LessonCall
      v-for="(call, i) of call_list" :key="call.id"
      v-bind:call="call"
      v-bind:index="i"
      v-on:SetPlay="SetPlay"
      v-on:deleteCall="deleteCall"
      v-on:updateValue="updateValue"
      />
    </ul>
</template>

<script>
import LessonCall from '@/components/Lesson/LessonCall.vue'
export default {
  props: ['call_list'],
  components: {
    LessonCall
  },
  methods: {
    SetPlay (id) {
      this.$emit('SetPlay', id)
    },
    deleteCall (id) {
      this.$emit('deleteCall', id)
    },
    updateValue (id, value, newValue) {
      this.$emit('updateValue', id, value, newValue)
    }
  }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>
