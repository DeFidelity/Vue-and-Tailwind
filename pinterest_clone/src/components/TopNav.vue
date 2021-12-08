<template>
  <div class="p-3 flex items-center justify-between">
      <div class="flex items-center">
        <button class="rounded-full bg-light p-3 flex items-center justify-center">
            <img src="../../public/logo.png" alt="logo" class="h-6 w-6">
        </button>
        <button v-for="item in tabitem" @click="selectedTab = item.key" :name="selectedTab" :key="item.key" type="" :class="{selectedTab: 'bg-dark text-white','text-dark hover:bg-light  rounded-full py-3 px-4 font-semibold':!selectedTab}">
            {{item.name}}
        </button>
      </div>

      <div class="flex-grow relative">
          <span class="material-icons absolute mt-3 ml-3 text-muted">search</span>
          <input class="rounded-full text-muted w-full hover:bg-lightHover bg-light py-3 pr-3 pl-10 hover:" placeholder="search" type="text">
      </div>

      <div class="flex items-center">
          <button class="rounded-full relative text-muted hover:bg-lightHover flex items-center justify-center p-3">
              <span class="material-icons text-3xl">notifications</span>
              <div class="rounded-full h-5 w-5 bg-primary text-white flex justify-center absolute mb-5 ml-5 ">4</div>
          </button>
          <button class="rounded-full text-muted relative hover:bg-lightHover flex items-center justify-center p-3">
              <span class="material-icons text-3xl">sms</span>
              <div class="rounded-full h-5 w-5 bg-primary text-white flex justify-center absolute mb-5 ml-5 ">2</div>
          </button>
          <button class="rounded-full bg-light p-3 flex items-center justify-center">
            <!-- <div class="w-6 h-6 bg-cover bg-center rounded-full" style="background-image:url(../assets/logo.png)"></div> -->
            <img src="../assets/logo.png" alt="logo" class="h-5 w-5">
        </button>
        <button class="w-6 h-6 hover:bg-light flex items-center justify-center">
            <div class="material-icons text-muted">expand_more</div>
        </button>
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return {
            tabitem: [
                {name: "Home", key:"home"},
                {name: "Today", key:"today"},
            ]
        }
    },
    selectedTab: 'home'
}
</script>

<style>

</style>