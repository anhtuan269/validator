<template>
  <div class="component">
    <h3>Information User Details</h3>
    <p>List Details</p>
    <p>My Name : {{ reversName() }}</p>
    <p>My Age : {{ userAge }}</p>
    <button @click="resetName">Reset Name</button>
    <button @click="resetNameFn()">Reset Name Callback</button>
  </div>
</template>

<script>
export default {
  // props dung de truyen du lieu tu component cha den component con, cac component con truyen tho

  props: {
    customName: {
      type: String,
      default: () => "Archie",
    },
    resetNameFn: Function,
    userAge: Number
  },
  methods: {
    reversName() {
      return this.customName.split("").reverse().join("");
    },
    resetName() {
      this.$emit("nameWasReset", "Archie");
      this.$emit("ageWasReset", 30);
    },
  },
};
</script>

<style scoped >
.component {
  background-color: lightcoral;
}
</style>