<script>
export default {
  name: "greet-developer",
  props: {
    firstName: String,
    lastName: String,
  },
  methods: {
    getGreeting(){
      if (!this.firstName?.trim() || !this.lastName?.trim()){
        return "Welcome Anonymous Developer";
      }
      const developer = new Developer(this.firstName, this.lastName);
      return `Congrats ${developer.fullName}! Now you are a Vue Developer`;
    }
  }
}
</script>
  <p>{{ getGreeting() }}</p>
<template>

</template>

<style scoped>

</style>