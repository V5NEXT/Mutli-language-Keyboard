<template>
  <div id="app">
<select class="form-select form-select-lg mb-3 form-control" aria-label=".form-select-lg example" name="LeaveType" v-model="leaveType" @change="onChangeLang()">
  <option value="english">English</option>
  <option value="german">German</option>
  <option value="french">French</option>
  <option value="spanish">Spanish</option>
    <option value="chinese">Chinese</option>

</select>

    <input
      :value="input"
      class="input"
      @input="onInputChange"
      placeholder="Tap on the virtual keyboard to start"
    >
    <SimpleKeyboard @onChange="onChange" @onKeyPress="onKeyPress" :input="input" :language="leaveType" ref="childComponent"/>
  </div>
</template>

<script>
import SimpleKeyboard from "./SimpleKeyboard.vue";
import "./App.css";

export default {
  name: "App",
  components: {
    SimpleKeyboard
  },

  data: () => ({
    input: "",
    leaveType: 'english',

  }),
  methods: {
    onChange(input) {
      this.input = input;
    },
       onChangeLang() {
            console.log('The new value is: ', this.leaveType)
            this.$refs.childComponent.setValue(this.leaveType)
        },
    onKeyPress(button) {
      
      // console.log("button", button);
    },
    onInputChange(input) {
      this.input = input.target.value;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
