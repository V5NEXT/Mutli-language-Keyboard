<template>
  <div>
    <div>
      <div class="simple-keyboard"></div>
    </div>


  </div>
</template>

<script>
import german from "simple-keyboard-layouts/build/layouts/german";
import english from "simple-keyboard-layouts/build/layouts/english";
import french from "simple-keyboard-layouts/build/layouts/french";
import spanish from "simple-keyboard-layouts/build/layouts/spanish";
import chinese from "simple-keyboard-layouts/build/layouts/chinese";


import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

export default {
  name: "SimpleKeyboard",
  props: {
     language : String
   },
  data: () => ({
    keyboard: null,
    layout: english,
  }),
  mounted() {
    this.createKeyboard();



  },
  activated(){
      this.keyboard.setOptions({ layout: this.language });
  },
  methods: {
    createKeyboard() {
      this.keyboard = new Keyboard({
        onChange: this.onChange,
        onKeyPress: this.onKeyPress,
        layout: this.layout,
      });

      this.setKeyboardInput(this.input);
    },
     setValue: function(value) {
        this.value = value;
        if(this.value == "english"){
                this.keyboard.setOptions({ layout: english });

        }
            else if(this.value == "german"){
                this.keyboard.setOptions({ layout: german });

        }
             else if(this.value == "french"){
                this.keyboard.setOptions({ layout: french });

        }
             else if(this.value == "spanish"){
                this.keyboard.setOptions({ layout: spanish });

        }
             else if(this.value == "chinese"){
                this.keyboard.setOptions({ layout: chinese });

        }

    },
    onChange(input) {
      this.$emit("onChange", input);
    },
    onKeyPress(button) {
      this.$emit("onKeyPress", button);

      if (button === "{shift}" || button === "{lock}") {
        this.handleShift();
      }
    },
    handleShift() {
      const currentLayout = this.keyboard.options.layoutName;
      const shiftToggle = currentLayout === "default" ? "shift" : "default";

      this.keyboard.setOptions({
        layoutName: shiftToggle,
      });
    },
    setKeyboardInput(input) {
      this.keyboard.setInput(input);
    },
    hideKeyboard() {
      this.$emit("closeKeyboard");
    },
  },
  watch: {
    input(input) {
      this.setKeyboardInput(input);
    },
  },
};
</script>

<style scoped>
button {
  background-color: tomato;
  border: none;
  border-radius: 4px;
  color: #fff;
  padding: 0.5em;
  cursor: pointer;
}
.hg-theme-default{
background: #642d82;
}
.hg-standardBtn{
  background: #322e2b!important;
}
.hg-button span{
  color: #fff;
}

</style>