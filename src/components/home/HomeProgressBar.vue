<template>
  <b-col>
    <p><b class="uppercase">{{ header }}:</b> {{ title }}</p>
      <b-progress :id="index" height="7px" :value="0"></b-progress>
    <br>
  </b-col>
</template>

<script>
export default {
  props: {
    header: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  }
}
</script>