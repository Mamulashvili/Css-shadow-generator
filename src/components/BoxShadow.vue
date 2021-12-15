<template>
  <div class="wrapper row">
    <div class="col-md-6 d-flex align-items-center">
      <div class="container">
        <div class="col-md-12">
          <base-range-input
            input-id="hlength"
            label-text="Horizontal length"
            @change-range="updateHorizontalLength"
            :initial-value="horizontalLength"
          />
          <base-range-input
            input-id="vlength"
            label-text="Vertical Length"
            @change-range="updateVerticalLength"
            :initial-value="verticalLength"
          />

          <base-range-input
            input-id="blurradius"
            label-text="Blur Radius"
            input-min="0"
            input-max="300"
            @change-range="updateBlurRadius"
            :initial-value="blurRadius"
          />

          <base-range-input
            input-id="spreadradius"
            label-text="Spread Radius"
            @change-range="updateSpreadRadius"
            :initial-value="spreadRadius"
          />

          <hr />

          <base-range-input
            input-id="borderRadius"
            label-text="Border Radius"
            input-min="0"
            input-max="200"
            @change-range="updateBorderRadius"
            :initial-value="borderRadius"
          />
          <hr />

          <base-color-input
            :input-id="boxColor"
            :input-name="boxColor"
            :initial-value="boxColor"
            @change-color="updateBoxColor"
            label-text="Box color"
          />
          <br />
          <base-color-input
            :input-id="shadowColor"
            :input-name="shadowColor"
            :initial-value="shadowColor"
            @change-color="updateShadowColor"
            label-text="Shadow color"
          />

          <hr />

          <base-switch
            input-id="switch"
            off-text="Outer shadow"
            on-text="Inner shadow"
            @handle-switch="changeShadowDirection"
          />
        </div>
      </div>
    </div>
    <div class="col-md-6 d-flex align-items-center">
      <div
        class="box"
        v-box-shadow:[shadowColor]="{
          shadowDirection,
          horizontalLength,
          verticalLength,
          blurRadius,
          spreadRadius,
        }"
        v-box-color="boxColor"
        v-box-border-radius="borderRadius"
      >
        <div class="generated-styles">
          <p>
            box-shadow: {{ shadowDirection ? "inset" : "" }}
            {{ horizontalLength }}px {{ verticalLength }}px {{ blurRadius }}px
            {{ spreadRadius }}px {{ shadowColor }};
          </p>
          <p>border-radius: {{ borderRadius }}px</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineAsyncComponent } from "vue";

const BaseRangeInput = defineAsyncComponent(() =>
  import("@/components/BaseRangeInput")
);

const BaseColorInput = defineAsyncComponent(() =>
  import("@/components/BaseColorInput")
);

const BaseSwitch = defineAsyncComponent(() =>
  import("@/components/BaseSwitch")
);

export default {
  name: "BoxShadow",
  components: {
    BaseRangeInput,
    BaseColorInput,
    BaseSwitch,
  },
  data() {
    return {
      horizontalLength: 10,
      verticalLength: 10,
      blurRadius: 5,
      spreadRadius: 0,
      borderRadius: 0,
      shadowColor: "#000000",
      boxColor: "#e7a61a",
      shadowDirection: false,
    };
  },

  methods: {
    updateHorizontalLength: function (val) {
      this.horizontalLength = val;
    },

    updateVerticalLength: function (val) {
      this.verticalLength = val;
    },

    updateBlurRadius: function (val) {
      this.blurRadius = val;
    },

    updateSpreadRadius: function (val) {
      this.spreadRadius = val;
    },

    updateBorderRadius: function (val) {
      this.borderRadius = val;
    },

    updateBoxColor: function (val) {
      this.boxColor = val;
    },

    updateShadowColor: function (val) {
      this.shadowColor = val;
    },

    changeShadowDirection: function (val) {
      this.shadowDirection = val;
    },
  },

  directives: {
    boxShadow: {
      created(el, binding) {
        let {
          shadowDirection,
          horizontalLength,
          verticalLength,
          blurRadius,
          spreadRadius,
        } = binding.value;

        shadowDirection = shadowDirection ? "inset" : "";
        el.style.boxShadow = `${shadowDirection} ${horizontalLength}px ${verticalLength}px ${blurRadius}px ${spreadRadius}px ${binding.arg}`;
      },

      updated(el, binding) {
        let {
          shadowDirection,
          horizontalLength,
          verticalLength,
          blurRadius,
          spreadRadius,
        } = binding.value;
        shadowDirection = shadowDirection ? "inset" : "";
        el.style.boxShadow = `${shadowDirection} ${horizontalLength}px ${verticalLength}px ${blurRadius}px ${spreadRadius}px ${binding.arg}`;
      },
    },

    boxColor: {
      updated(el, binding) {
        el.style.backgroundColor = binding.value;
      },
    },

    boxBorderRadius: {
      updated(el, binding) {
        el.style.borderRadius = binding.value + "px";
      },
    },
  },
};
</script>

<style scoped>
.wrapper {
  width: 80%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: auto;
  margin-top: 5rem;
}

.box {
  width: 400px;
  height: 400px;
  background-color: rgb(231, 166, 26);
  display: flex;
  align-items: center;
  justify-content: center;
}

.generated-styles {
  background-color: #ddd;
  padding: 1.5rem;
  width: 80%;
  margin: auto;
}

.box p {
  text-align: left;
  margin-bottom: 0.3rem;
}

@media (max-width: 761px) {
  .box {
    margin: 50px 0;
    width: 100%;
    height: 200px;
  }
}
</style>
