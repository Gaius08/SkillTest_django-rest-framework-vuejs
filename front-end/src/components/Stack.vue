<template>
    <div>
      <v-row v-for="(stack, index) in stacks" :key="index">
        <v-btn 
          class="mt-4 list" 
          elevation="4"
          :class="{ 'active': activeIndex === index }"
          @click="setActive(index)"
        >
          <h3>{{ stack.title }}</h3>
        </v-btn>
      </v-row>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Stacks',
    props: {
      stacks: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        activeIndex: null
      }
    },
    methods: {
      setActive(index) {
        this.activeIndex = index
      }
    }
  }
  </script>
  
  <style>
  .list {
    width: 400px;
  }
  .list:hover {
    background-image: linear-gradient(to bottom right, #eb87d5, #86baee);
  }
  .active {
    background-image: linear-gradient(to bottom right, #eb87d5, #86baee);
    color: white;
  }
  </style>
  