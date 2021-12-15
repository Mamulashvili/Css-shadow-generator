<template>
  <div class="flex flex-spc-btwn">
    <span :for="inputId"> {{ offText }} </span>
    <div class="checkbox-wrapper">
      <input
        type="checkbox"
        :id="inputId"
        :checked="checkbox"
        @input="changeSwitch"
      />
      <label :for="inputId"></label>
    </div>
    <span :for="inputId"> {{ onText }}</span>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  props: {
    inputId: {
      type: String,
      required: true,
    },

    onText: {
      type: String,
      required: true,
    },

    offText: {
      type: String,
      required: true,
    },
  },
  emits: ["handleSwitch"],
  setup(_, { emit }) {
    const checkbox = ref(false);

    function changeSwitch(e) {
      checkbox.value = e.target.checked;
      emit("handleSwitch", checkbox);
    }

    return {
      checkbox,
      changeSwitch,
    };
  },
};
</script>

<style scoped>
input[type="checkbox"] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label {
  cursor: pointer;
  text-indent: -9999px;
  width: 50px;
  height: 25px;
  background: grey;
  display: block;
  border-radius: 100px;
  position: relative;
}

label:after {
  content: "";
  position: absolute;
  /* top: 5px; */
  left: 0;
  width: 25px;
  height: 25px;
  background: #ddd;
  border-radius: 90px;
  transition: 0.3s;
}

input:checked + label {
  background: #bada55;
}

input:checked + label:after {
  left: calc(100%);
  transform: translateX(-100%);
}

label:active:after {
  width: 80%;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.checkbox-wrapper {
  margin-top: -20px;
}
</style>
