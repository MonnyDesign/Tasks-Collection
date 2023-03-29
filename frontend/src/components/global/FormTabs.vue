<template>
  <div class="grid grid-cols-12 lg:gap-12 py-10">
    <!-- Left Side Content -->
    <div class="col-span-full lg:col-span-4">
      <h1 class="text-2xl font-semibold ">Task List</h1>

      <!-- Search Field -->
      <input
        class="search-input w-full block border-2 border-gray-200 p-2 my-3 rounded-md"
        placeholder="Search..."
        v-model="filterTaskValue"
      />

      <!-- Tasks List / Named tasks -->
      <ul class="tabs">
        <li class="tab mb-4 pl-4 relative" v-for="(task, i) in filteredTaskList" 
        @click.stop.prevent="selectTab(i, task)" :class="[{'active': activeIndex === i}]" :key="i">
          <a class="border-gray-200 border-b-2 block py-3" href="#">
            <span class="title text-xl font-medium block">{{ task.name }}</span>
            <span>{{ task.subHeading }}</span>
          </a>
        </li>
      </ul>
    </div>
    
    <!-- Right Side Content -->
    <div class="col-span-full lg:col-span-8">
      <!-- Tasks Content / Opened tasks content -->
      <div class="tabs-content pt-10 lg:pt-0 block">
          <h2 class="text-2xl font-semibold">{{ selectedTask.name }}</h2>
            <form class="grid grid-cols-12 gap-4" ref="form">
            
              <div v-for="(field, i) in selectedTask.fields" :key="i" 
                :class="[`lg:col-span-${field.size.lg}`, `md:col-span-${field.size.md}`, `sm:col-span-${field.size.sm}`, 'col-span-full']">

              <!-- Dispay content with type 'paragraph' -->
              <template v-if="field.type == 'paragraph'">
                <simple-text-content :content="field.content" />
              </template>

              <!-- Dispay input field with type 'inputText' -->
              <input-field v-if="field.type == 'inputText' "
                v-model:modelValue="formData[field.name]"
                :inputId="field.id" 
                :inputName="field.name"
                :label="field.label" 
                :min="field.validation.min" 
                :max="field.validation.max"
                :isRequired="!field.optional"
                :disabledInput="this.disabledForm[this.selectedTask.id]"
              />

              <!-- Dispay input field with type 'inputDocument' -->
              <input-upload-field v-if="field.type == 'inputDocument'"
                v-model:modelValue="formData[field.name]"
                :accceptFile="field.validation.acceptType + '/*'"
                :inputId="field.id"
                :inputName="field.name"
                :label="field.label" 
                :min="field.validation.min" 
                :max="field.validation.max"
                :inputType="'file'"
                :isRequired="!field.optional"
                :disabledInput="this.disabledForm[this.selectedTask.id]"
              />

              <!-- Dispay input field with type 'inputSelect' -->
              <select-option-field v-if="field.type == 'inputSelect'"
                v-model:modelValue="formData[field.name]"
                :inputId="field.id"
                :inputName="field.name"
                :dataset="field"
                :label="field.label"
                :isRequired="!field.optional"
                :disabledInput="this.disabledForm[this.selectedTask.id]"
              />

              <!-- Dispay input field with type 'inputTextArea' -->
              <text-area-field v-if="field.type == 'inputTextArea'"
                v-model:modelValue="formData[field.name]"
                :inputId="field.id"
                :inputName="field.name"
                :label="field.label"
                :isRequired="!field.optional"
                :disabledInput="this.disabledForm[this.selectedTask.id]"
              />
            </div>
            
            <!-- Dispay button if there is/are a form field/s -->
            <template  v-if="this.isForm">
              <button type="button" class="uppercase mt-4 col-span-1" @click="submit">
                <span class="p-4 bg-blue-500 rounded-md text-white hover:opacity-80 transition-opacity ">Submit</span>
              </button>
            </template>

          </form>

      </div>
    </div>
  </div>
</template>

<script>
import SimpleTextContent from '../templates/SimpleTextContent'
import InputField from '../templates/InputField'
import SelectOptionField from '../templates/SelectOptionField'
import TextAreaField from '../templates/TextAreaField'
import InputUploadField from '../templates/InputUploadField'


export default{
  el: '#root',
  data() {
    return {
      activeIndex:0,
      tasksCollectionList:[],
      selectedTask: {},
      filterTaskValue: '',
      formData: {},
      isForm: false,
      disabledForm: {}
    };
  },

  components:{
    SimpleTextContent,
    InputField,
    SelectOptionField,
    TextAreaField,
    InputUploadField
  },

  // Extracting the data
  beforeMount(){
    fetch('http://localhost:3000/tasks')
    .then((response) => response.json())
    .then((response) => this.tasksCollectionList = response.data)
    .then((tasks) => this.selectTab(0, tasks[0]))
    .then((response) => console.log('tasksCollectionList: ' , response));
  },

  methods: {
    selectTab(index, task){
      this.activeIndex = index;

      fetch('http://localhost:3000/tasks/' + task.id)
      .then((response) => response.json())
      .then((response) => this.selectedTask = response.data[0])
      .then((task) => this.isForm = task.fields.some((field) => field.type === 'inputText' || field.type === 'inputDocument' || field.type === 'inputSelect' || field.type === 'inputTextArea'))
      .then((response) => console.log('selectedTask: ' , response)); 
    },
    // Submit form data
    submit : function(){
      const formData = new FormData(this.$refs.form);
      const data = Object.fromEntries(formData);
      this.disabledForm[this.selectedTask.id] = true;
      fetch('http://localhost:3000/tasks/' + this.selectedTask.id, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(data)
      });
    }
  },
  computed: {
    // Filter/Search function
    filteredTaskList: function () {
      return this.tasksCollectionList.filter(item => {
        return item.name.toLowerCase().indexOf(this.filterTaskValue) !== -1 || item.subHeading.toLowerCase().indexOf(this.filterTaskValue) !== -1;
      });
    },
  },
}
</script>

<style lang="scss" scoped>
  .tab{
    &.active,
    &:hover{
      @apply w-full inline-block;
      background-color: #daf5ff;
      transition: background-color 0.4s;

      .title{
        @apply text-blue-500;
      }

      a{
        &:before{
          @apply border-blue-500;
          transition: border-color 0.4s;
          
        }
      }
    }

    a{
      &:before{
        content: '';
        width: 15px;
        height: 15px;
        position: absolute;
        border-right: 2px solid #ccc;
        border-top: 2px solid #ccc; 
        transform: translateY(-50%) rotate(135deg);
        right: 0;
        top: 50%;
        @apply mr-4;
        @screen lg{
          transform: translateY(-50%) rotate(45deg);
        }
      }
    }
  }
  .search-input{
    @apply relative;
    &:after{
      content: '';
      background: url('../../../assets/imgs/search-icon.png') no-repeat;
      position: absolute;
      right: 1rem;
      top: 25%;
      width: 100%;
      height: 100%;
    }
  }
</style>