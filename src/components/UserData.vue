<template>
  <div>
    <h2>{{ userName }}</h2>
    <h3>{{ age }}</h3>
  </div>
</template>

<script>
import {
  computed,
  inject,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
} from 'vue';

export default {
  props: ['firstName', 'lastName'],
  // computed: {
  //     userName () {
  //         return this.firstName + ' ' + this.lastName;
  //     }
  // }
  setup(props, context) {
    const uName = computed(() => {
      return props.firstName + ' ' + props.lastName;
    });

    // se recomienda cambiar valores inject desde el lugar donde lo creamos provide
    const age = inject('userAge');

    console.log(context);
    
    onBeforeMount(() => {
        console.log('onBeforeMount');
    })

    onMounted(() => {
        console.log('onMounted');
    })

    onBeforeUpdate(() => {
        console.log('onBeforeUpdate');
    })

    onUpdated(() => {
        console.log('onUpdated');
    })

    onBeforeUnmount(() => {
        console.log('onBeforeUnmount');
    })

    onUnmounted(() => {
        console.log('onUnmounted');
    })

    // Forma de usar emit en Composition API, por medio de context
    // context.emit('save-data', 1); // this.$emit('save-data', 1);
    return { userName: uName, age };
  },
};
</script>