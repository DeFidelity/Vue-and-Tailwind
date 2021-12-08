<template>
  <div class="relative" @mouseover="hover=true" @mouseleave="hover=false">
      <img :src="src" class="rounded-lg" alt="">

      <div v-if="hover" class="absolute bg-dark opacity-50 inset-0 w-full h-full rounded-lg"></div>
      <div class="absolute top-0 w-full h-full flex flex-col justify-between p-3">
          <div v-if="hover" class="flex items-center justify-between">
              <button type="button" class="flex items-center" name="button">
                  <p class="font-semibold text-white">{{board}}</p>
                  <div class="material-icons text-white">expand_more</div>
              </button>
              <button class="rounded-full font-semibold bg-primary px-5 text-white py-3">
                  Save
                </button>
          </div>
          <div class="flex items-center w-full">
              <button class="ml-auto bg-white text-dark rounded-full w-8 h-8 flex-items-center justify-center mr-2 opacity-70 hover:opacity-100">
                  <span class="material-icons text-base">ios_share</span>
              </button>
              <button class="bg-white text-dark rounded-full w-8 h-8 flex-items-center justify-center opacity-75 hover:opacity-100">
                  <span class="material-icons text-base">more_horiz</span>
              </button>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    props: ['src','board'],
    data() {
        return {
            hover: false
        }
    }
}
</script>

<style>

</style>