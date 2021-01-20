<template>
  <h2>{{ userName }}</h2>
  <h3>{{ age }}</h3>
</template>

<script>
import { computed } from 'vue';
export default {
  props: ['firstName', 'lastName', 'age'],
  // computed: {
  //     userName () {
  //         return this.firstName + ' ' + this.lastName;
  //     }
  // }
  setup(props, context) {
    const uName = computed(() => {
      return props.firstName + ' ' + props.lastName;
    });

    console.log(context);

    // Forma de usar emit en Composition API, por medio de context
    // context.emit('save-data', 1); // this.$emit('save-data', 1);
    return { userName: uName };
  },
};
</script>