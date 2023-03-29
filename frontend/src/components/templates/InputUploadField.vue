<template>
  <div class="input-upload py-1 lg:py-3">
    <p class="capitalize mb-1">{{ label }}</p>
    <label class="py-5 block border-2 w-full border-gray-200 px-2 mt-1 rounded-md" :id="inputId" > 
      <input 
        :type="inputType" 
        :accept="accceptFile" 
        :required="isRequired" 
        :minlength="min" 
        :maxlength="max" 
        :id="inputId" 
        :name="inputName"
        :value="modelValue"
        :disabled="disabledInput"
       @input="$emit('update:modelValue', $event.target.value)" />
    </label>
  </div>
</template>

<script>
export default {
  props: {
    inputId: { 
      type: String, 
      default: "text" 
    },
    inputName: { 
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

<style lang="scss" scoped>
  .input-upload{
    label{
      @apply relative cursor-pointer ;
      &:before{
        content: '';
        background: url('../../../assets/imgs/attach.png') no-repeat;
        position: absolute;
        left: 1rem;
        top: 23%;
        width: 100%;
        height: 100%;
      }
    }
    input{
      @apply hidden;
    }
  }
</style>