<template>
  <div class="flex flex-spc-btwn">
    <label :for="inputId">{{ labelText }}</label>
    <span>{{ range }} px</span>
  </div>
  <input
    type="range"
    class="form-range"
    :name="inputName"
    :id="inputId"
    @input="updateRange"
    :min="inputMin"
    :max="inputMax"
    :value="range"
  />
</template>

<script>
export default {
  props: {
    inputName: {
      type: String,
      required: false,
      default: "",
    },
    inputId: {
      type: String,
      required: true,
    },
    labelText: {
      type: String,
      required: false,
    },
    inputMin: {
      type: [Number, String],
      required: false,
      default: -200,
    },
    inputMax: {
      type: [Number, String],
      required: false,
      default: 200,
    },
    initialValue: {
      type: [Number, String],
      required: false,
      default: 0,
    },
  },
  emits: ["changeRange"],
  data() {
    return {
      range: 0,
    };
  },
  methods: {
    updateRange(event) {
      this.range = event.target.value;
      this.$emit("changeRange", this.range);
    },
  },
  mounted() {
    this.range = this.initialValue;
  },
};
</script>

<style scoped>
label,
span {
  font-weight: 500;
}
</style>
