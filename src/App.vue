<template>
  <section class="container">
    <user-data :first-name="firstName" :last-name="lastName" :age="age">
    </user-data>
    <button @click="setAge">Add Age</button>
    <div>
      <!-- v-model reconoce los argumentos pasados como refs -->
      <input type="text" placeholder="First Name" v-model="firstName" />
      <!-- ref tambien puede ser accedido desde setup funcion -->
      <input type="text" placeholder="Last Name" ref="lastNameInput" />
      <button @click="setLastName">Set last Name</button>
    </div>
  </section>
</template>

<script>
import { ref, computed, watch } from 'vue';
import UserData from './components/UserData.vue';
export default {
  components: {
    UserData,
  },
  setup() {
    // const uName = ref('Sergio');
    const firstName = ref('');
    const lastName = ref('');
    const lastNameInput = ref(null);
    const uAge = ref(23);

    // reactive only works with objects
    // const user = reactive({
    //   name: 'Sergio',
    //   age: 23,
    // });

    // computed properties generan variables de tipo ref de 'solo lectura'
    // los ref normales generan variables de lectura y escritura
    const uName = computed(function () {
      return firstName.value + ' ' + lastName.value;
    });

    // uso del watch en setup composition api
    watch([uAge, uName], function (newValues, oldValues) {
      console.log('Old age: ' + oldValues[0]);
      console.log('New Age: ' + newValues[0]);
      console.log('Old Name: ' + oldValues[1]);
      console.log('New Name: ' + newValues[1]);
    });

    function setNewAge() {
      uAge.value += 1;
    }

    function setLastName() {
      // el primer value es del ref de setup y el segundo del template el cual accede
      lastName.value = lastNameInput.value.value;
    }

    // function setFirstName(event) {
    //   firstName.value = event.target.value;
    // }

    // function setLastName(event) {
    //   lastName.value = event.target.value;
    // }

    // Recordatorio cuando se pase un solo valor como setFirstName (actualizacion firstName) usamos,
    // shortcuts modernos de Javascript el cual en realidad es setFirstName: setFirstName
    return {
      userName: uName,
      age: uAge,
      setAge: setNewAge,
      firstName,
      lastName,
      lastNameInput,
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