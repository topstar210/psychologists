<template>
  <div class="custom-select" :tabindex="tabindex" @blur="open = false">
    <div
      class="flex gap-2 items-center selected bg-gray-50"
      :class="{ open: open }"
      @click="open = !open"
    >
      <img v-if="icon" :src="icon" class="w-4" alt="icon" />
      <div class="w-2/3 overflow-hidden h-[45px]"><div>{{ selected }}</div></div>
    </div>
    <div class="items" :class="{ selectHide: !open }">
      <div
        v-for="(option, i) of options"
        :key="i"
        @click="
          selected = option;
          open = false;
          $emit('input', option);
        "
      >
        {{ option }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      required: true,
    },
    default: {
      type: String,
      required: false,
      default: null,
    },
    tabindex: {
      type: Number,
      required: false,
      default: 0,
    },
    icon: {
      type: String,
    },
  },
  data() {
    return {
      selected: this.default
        ? this.default
        : this.options.length > 0
        ? this.options[0]
        : null,
      open: false,
    };
  },
  mounted() {
    // this.$emit("input", this.selected);
    if(this.resetVal){
      this.resetVal();
    }
  },
  watch: {
    ["default"]: {
      handler: function (newVal, oldVal) {
        this.selected = this.default;
      },
      deep: true,
    },
  },
};
</script>

<style scoped>
.custom-select {
  position: relative;
  width: 100%;
  text-align: left;
  outline: none;
  height: 45px;
  line-height: 45px;
}

.custom-select .selected {
  background-color: white;
  border-radius: 6px;
  border: 1px solid rgb(209, 213, 219);
  color: #000;
  padding-left: 1em;
  cursor: pointer;
  user-select: none;
}

.custom-select .selected.open {
  border: 1px solid rgb(209, 213, 219);
  border-radius: 6px 6px 0px 0px;
}

.custom-select .selected:after {
  position: absolute;
  content: "";
  top: 22px;
  right: 1em;
  width: 0;
  height: 0;
  border: 5px solid transparent;
  border-color: rgb(209, 213, 219) transparent transparent transparent;
}

.custom-select .items {
  color: #000;
  background-color: #fff;
  overflow: hidden;
  border-right: 1px solid rgb(209, 213, 219);
  border-left: 1px solid rgb(209, 213, 219);
  border-bottom: 1px solid rgb(209, 213, 219);
  position: absolute;
  left: 0;
  right: 0;
  z-index: 1;
}

.custom-select .items div {
  color: #000;
  padding-left: 1em;
  cursor: pointer;
  user-select: none;
}

.custom-select .items div:hover {
  background-color: #d8d8d8;
}

.selectHide {
  display: none;
}
</style>
