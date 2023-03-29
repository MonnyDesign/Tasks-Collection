<template>
  <label class="capitalize py-2 lg:py-4 block" :for="inputId"> {{ label }} 
    <input class="border-2 w-full border-gray-200 p-2 mt-1 rounded-md"
      :type="inputType"
      :required="isRequired" 
      :minlength="min" 
      :maxlength="max"
      :id="inputId"
      :name="inputName"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      :disabled="disabledInput" >
  </label>
</template>

<script>
export default {
  props: {
    inputId: { 
      type: String, Number
    },
    inputName: { 
      type: String
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
    accceptFile: {
      type: String
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