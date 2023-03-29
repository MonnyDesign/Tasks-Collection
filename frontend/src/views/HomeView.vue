<template>
  <div class="px-6 lg:px-10 border-2 border-gray-200">

    <!-- To Do List-->
    <div>
      <form-tabs />
    </div>
  </div>
</template>

<script>
import FormTabs from '../components/global/FormTabs';


export default {
  name: 'HomeView',
  components: {
    FormTabs,
  }
}
</script>
