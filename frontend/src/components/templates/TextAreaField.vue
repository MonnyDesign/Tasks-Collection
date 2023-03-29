<template>
  <label class="capitalize py-2 lg:py-4 block" :for="inputId"> {{ label }} 
    <textarea class="border-2 w-full border-gray-200 p-2 mt-1 rounded-md h-60 " 
      :id="inputId"
      :row="rows"
      :col="cols"
      :type="inputType"
      :required="isRequired" 
      :minlength="min" 
      :maxlength="max" 
      :value="modelValue"
      :disabled="disabledInput"
      @input="$emit('update:modelValue', $event.target.value)" >
    </textarea>
  </label>
</template>

<script>
export default {
  props: {
    id: { 
      type: String, 
      default: "text" 
    },
    name: { 
      type: String, 
      default: null 
    },
    label: {
      type: String,
      default: ""
    },
    min: {
      type: Number
    },
    max: {
      type: Number
    },
    inputType: {
      type: String, 
      default: "text"
    },
    isRequired: {
      type: Boolean,
      default: true
    },
    rows: { 
      type: Number, 
      default: 15 
    },
    cols: { 
      type: Number
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