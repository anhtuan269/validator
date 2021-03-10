<template>
  <div class="component">
      <h3>
          You may edit user here
      </h3>
      <p> Edit me</p>
      <p>My age: {{userAge}}</p>
      <button @click="editAge"> Change Age </button>
      <button @click="resetAgeFn()"> Reset Age </button>
  </div>
</template>

<script>
export default {
    props: {
        userAge: Number,
        resetAgeFn: Function
    },
    methods: {
        editAge(){
            this.$emit('update:age',18) ;
            this.$emit('update:name', 'Quach Thanh vu')
        },
        resetAge(){
            this.$emit("nameWasReset", "Archie");
            this.$emit("ageWasReset", 30);
        }
    }
}
</script>

<style scoped>
    .component {
        background-color: lightgreen;
    }
</style>