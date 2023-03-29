<template>
  <label class="capitalize py-2 lg:py-4 block relative" :for="inputId"> {{ label }}  
    <select class="border-2 w-full border-gray-200 px-2 py-3 mt-1 rounded-md relative" 
      :name="inputName" 
      :id="inputId" 
      :disabled="disabledInput"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)">
      <option selected disabled hidden>Select Country</option>
      <option v-for="(opt, i) in dataset.options" :key="i" :value="opt.value" >{{ opt.label }}</option>
    </select>
    <div class="arrow-select"></div>
  </label>
</template>

<script>
export default {
  data: () => ({

  }),
  props: {
    inputId: { 
      type: String, Number,
      default: null 
    },
    inputName: { 
      type: String, Number,
      default: null 
    },
    label: {
      type: String,
      default: ""
    },
    inputType: {
      type: String
    },
    isRequired: {
      type: Boolean
    },
    dataset: {
      type: [Object, Array]
    },
    modelValue:{
      type: String
    },
    disabledInput: {
      type: Boolean
    }
  }
}
</script>

<style lang="scss" scoped>
  select{
    position:relative;
    appearance: none;
  }

.arrow-select{
  width: 10px;
  height: 10px;
  position: absolute;
  transform: translateY(-63%) rotate(45deg);
  top: 63%;
  @apply border-r-2 border-b-2 border-black-500 right-4 lg:right-6 ;
}
</style>