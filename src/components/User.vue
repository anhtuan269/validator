<template>
  <div class="component mt-5">
    <h1>The User Component</h1>
    <p>My name is {{ name }} and i'm {{age}} years old</p>
    <button @click="changeName">Change my name</button>
    <hr />
    <div class="row">
      <div class="col-xs-12 col-sm-6">
        <user-detial 
          :customName="name"  
          @nameWasReset="name = $event" 
          @ageWasReset=" age = $event"
          :resetNameFn="resetName"  
          :userAge="age"

        />
      </div>
      <div class="col-xs-12 col-sm-6">
        <user-edit 
          @ageWasReset=" age = $event"
          :userAge="age"
          @update:age="age = $event"
          @update:name="name = $event"
          :resetAgeFn="resetAge"
        />
      </div>
    </div>
  </div>
</template>

<script>
import UserDetial from "../components/UserDetial.vue";
import UserEdit from "../components/UserEdit.vue";
export default {
  data() {
    return {
      name: "Archie",
      age: 30
    };
  },
  methods: {
    changeName: function () {
      this.name = "Quach Thanh Vu";
      this.age= 18;
    },
    resetName() {
      this.name = "Archie";
      this.age =30;
    },
    resetAge(){
      this.age=30
    }
  },

  components: { UserEdit, UserDetial },
};
</script>
<style>
.component {
  padding: 50px;
  max-width: 1200px;
  margin: auto;
  background-color: lightblue;
}
.component h1,
h3 {
  font-size: 50px;
}
.component p {
  font-size: 20px;
}
.component button {
  font-size: 18px;
  padding: 0px 20px;
  display: block;

}
.component button:not(:first-child){
  margin-top:20px;
}
</style>