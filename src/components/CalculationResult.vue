<template>
    <div v-if="age" class="">
      <p>You are {{ age.years }} years, {{ age.months }} months, and {{ age.days }} days old.</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      age: Object
    }
  }
  </script>