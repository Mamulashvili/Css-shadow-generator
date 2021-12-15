<template>
  <div class="flex flex-spc-btwn">
    <label :for="inputId">{{ labelText }}</label>
    <span>{{ color }}</span>
  </div>
  <input
    type="color"
    :name="inputName"
    :id="inputId"
    class="form-control form-control-color"
    :value="color"
    v-bind="$attrs"
    @input="changeColorHandler"
  />
</template>

<script>
import { toRefs } from "vue";

export default {
  name: "BaseColorInput",
  props: {
    inputId: {
      type: String,
      required: true,
    },
    inputName: {
      type: String,
      required: false,
    },
    initialValue: {
      type: String,
      required: true,
    },
    labelText: {
      type: String,
      required: true,
    },
    emits: ["changeColor"],
  },
  setup(props, context) {
    let { initialValue: color } = toRefs(props);

    function changeColorHandler(e) {
      color = e.target.value;
      context.emit("changeColor", color);
    }

    return {
      color,
      changeColorHandler,
    };
  },
};
</script>

<style scoped>
input {
  width: 100%;
}

label,
span {
  font-weight: 500;
}
</style>
