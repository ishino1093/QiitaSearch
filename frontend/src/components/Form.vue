<template>
  <div class="form">
    <div>
      <p class="caption">{{ inputCaption }}</p>
    </div>
    <input class="input" v-model="inputComputed" />
    <button class="button" @click="HandleClick">{{ buttonCaption }}</button>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType, reactive } from "vue";

export default defineComponent({
  name: "Form",

  props: {
    input: {
      type: String as PropType<string>,
      default: "",
    },
    inputCaption: {
      type: String as PropType<string>,
      default: "input",
    },
    buttonCaption: {
      type: String as PropType<string>,
      default: "button",
    },
  },
  emits: ["update-input", "button-click"],
  setup(props, { emit }) {
    // type
    type input = string;
    type UpdateInput = () => void;
    type HandleClick = () => void;

    const inputComputed = computed({
      get: () => {
        return props.input;
      },
      set: (val) => {
        emit("update-input", val);
      },
    });

    const HandleClick = () => {
      emit("button-click");
    };
    return {
      inputComputed,
      HandleClick,
    };
  },
});
</script>

<style scoped lang="scss">
$green: #88ac8f;
$green-hover: #95aa99;
$green-line: #7fab87;
$grey: #505050;

.form {
  margin: 15px;
}

.caption {
  position: relative;
  display: inline-block;
  left: -80px;
  margin: 0;
  color: $grey;
  font-size: 8px;
  font-weight: bold;
}

.input {
  color: $grey;
  border-radius: 5px;
  border: 1px solid $green-line;
}

.input:focus {
  border: 2px solid $green-line !important;
  outline: 0;
}

.button {
  background: $green;
  border: 1px solid $green;
  color: white;
  padding: 2px 5px;
  font-size: 12px;
  margin-left: 5px;
  border-radius: 5px;
}

.button:hover {
  background: $green-hover;
  border: 2px solid $green-hover;
}
.button:focus {
  border: 1px solid $green;
  outline: 0;
}
</style>
