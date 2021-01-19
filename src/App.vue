<template>
  <section class="container">
    <h2>{{ userName }}</h2>
    <h3>{{ age }}</h3>
    <button @click="setAge">Add Age</button>
    <div>
      <input type="text" placeholder="First Name" @input="setFirstName" />
      <input type="text" placeholder="Last Name" @input="setLastName" />
    </div>
  </section>
</template>

<script>
import { ref, computed } from 'vue';
export default {
  setup() {
    // const uName = ref('Sergio');
    const firstName = ref('');
    const lastName = ref('');
    const uAge = ref(23);

    // reactive only works with objects
    // const user = reactive({
    //   name: 'Sergio',
    //   age: 23,
    // });

    // computed properties generan variables de tipo ref de 'solo lectura'
    // los ref normales generan variables de lectura y escritura
    const uName = computed(function() {
      return firstName.value + ' ' + lastName.value;
    });

    function setNewAge() {
      uAge.value += 1;
    }

    function setFirstName(event) {
      firstName.value = event.target.value;
    }

    function setLastName(event) {
      lastName.value = event.target.value;
    }

    // Recordatorio cuando se pase un solo valor como setFirstName usamos,
    // shortcuts modernos de Javascript el cual en realidad es setFirstName: setFirstName
    return {
      userName: uName,
      age: uAge,
      setAge: setNewAge,
      setFirstName,
      setLastName,
    };
  },

  // data() {
  //   return {
  //     userName: 'Maximilian',
  //   };
  // },
  // methods: {
  //   setNewAge(){
  //     this.age = 24;
  //   }
  // }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

.container {
  margin: 3rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  text-align: center;
}
</style>