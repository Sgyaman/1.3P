<!-- Component.vue -->

<template>
    <div>
      <p>{{ message }}</p>
      <button @click="emitEvent">Click me</button>
    </div>
    <div>
    <h3>SIT120 Components SLOT</h3>
    <slot></slot>
  </div>
  </template>
  
  <script>
  export default {
    props: {
      message: String, // Define a prop named 'message'
    },
    methods: {
      emitEvent() {
        // Emit an event named 'childEvent'
        this.$emit('childEvent', 'Event data from child');
      },
    },
  };
  </script>
  

