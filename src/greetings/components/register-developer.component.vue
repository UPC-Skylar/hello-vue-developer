<script>
export default {
  name: "register-developer",
  emits: ['developer-registered', 'later'], //son los eventos que emite
  //caracteristicas internas q tendra el componente, atributos internos
  data(){
    return {
      firstName: "",
      lastName: "",
      errorMessage: "",
    }
  },
  //Metodos que contiene el componente
  methods: {
    clearForm(){
      this.firstName = "";
      this.lastName = "";
      this.errorMessage = "";
    },
    onRegister(){
      if(this.firstName.trim() || this.lastName.trim()){
        console.log("Registering developer");
        //Asi se emite un evento, el primer param es el nombre del elemento
        //el segundo parametro son los datos con los q viaja
        this.$emit('developer-registered', {
          firstName: this.firstName,
          lastName: this.lastName,
        });
        this.clearForm();
      } else {
        console.log("Cannot register: Both fields are required");
        this.errorMessage = "Please provide at least first name or last name. Warning: Both are required for a successful registration.";
      }
    },
    onLater(){
      console.log("Deffering registration");
      this.$emit('later', {
        firstName: this.firstName,
        lastName: this.lastName,
      });
      this.clearForm();
    }
  }
}
</script>

<template>
  <div>
    <h2>New Developer</h2>
    <div>
      <form v-on:submit.prevent="onRegister">
        <div class="field">
          <!-- v-model sirve para vincular componentes -->
          <label for="firstName">First Name:</label>
          <input id="firstName" v-model="firstName" type="text"/>
        </div>
        <div class="field">
          <label for="lastName">Last Name:</label>
          <input id="lastName" v-model="lastName" type="text"/>
        </div>
        <div class="actions">
          <button type="submit">Register</button>
          <button type="button" @click="onLater">Later</button>
          <button type="button" @click="clearForm">Clear</button>
        </div>
      </form>
      <p class="error" v-if="errorMessage" role="alert">{{errorMessage}}</p>
    </div>
  </div>
</template>

<style scoped>
button {
  margin-right: 10px;
  padding: 8px 16px;
  cursor: pointer;
}

.error{
  color: red;
  margin-top: 10px;
  font-size: 14px;
}

.field {
  margin-bottom: 10px;
}

.actions {
  margin-top: 10px;
}

label {
  margin-right: 5px;
}
</style>