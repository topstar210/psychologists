<template>
  <div class="relative">
    <img v-if="icon" :src="icon" class="w-4 absolute top-4 left-3" alt="icon" />
    <input
      type="text"
      v-model="inputVal"
      class="border border-gray-300 rounded-md block w-full p-2.5" :class="{'px-8':icon}"
      :placeholder="placeholder"
    />
  </div>
</template>

<script>
export default {
  props: {
    icon: {
        type: String,
    },
    placeholder:{
        type: String,
    },
    default: {
      type: String,
      required: false,
      default: null,
    },
  },
  data(){
    return{
        inputVal: this.default
    }
  },
  watch: {
    ["default"]: {
      handler: function (newVal, oldVal) {
        this.inputVal = this.default;
      },
      deep: true,
    },
  },
};
</script>
