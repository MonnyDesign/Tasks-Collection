<template>
  <div>
    <div class="bg-blue-500 py-4 px-6">
      <div class="logo lg:w-1/12 w-1/6">
        <img src="../../../../frontend/assets/imgs/logo-max.png" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    customStyle(){
      return {
        backgroundImage: `url('../../../../frontend/assets/imgs/logo-max.png')`,
      }
    }
  }
}
</script>