<template>
  <div class="component">
    <h1>The User Component</h1>
    <p>I'm an awesome user!</p>
    <!-- check with this @nameWasReset-->
    <p>Name is {{name}}</p>
    <p>Age is {{age}}</p>
    <!--  -->
    <button @click="changeName">Change my name</button>
    <hr />
    <div class="row">
      <div class="col-xs-12 col-sm-6">
        <app-user-detail
          :myName="name"
          @nameWasReset="name = $event"
          :resetFn="resetName"
          :userAge="age"
        ></app-user-detail>
      </div>
      <div class="col-xs-12 col-sm-6">
        <app-user-edit :userAge="age" @ageWasEdited="age = $event"></app-user-edit>
      </div>
    </div>
  </div>
</template>

<script>
import UserDetail from "./UserDetail";
import UserEdit from "./UserEdit";
export default {
  data: function () {
    return {
      name: "Fulano",
      age: 20,
    };
  },
  methods: {
    changeName() {
      this.name = "Cosme";
    },
    resetName() {
      this.name = "Fulano";
    },
  },
  components: {
    "app-user-edit": UserEdit,
    "app-user-detail": UserDetail,
  },
};
</script>

<style>
</style>