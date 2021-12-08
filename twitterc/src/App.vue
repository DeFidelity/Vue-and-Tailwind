<template>
<div class="flex h-screen container w-full">
  <!-- side nav -->
  <div class="lg:w-1/5 border-r border-lighter flex flex-col justify-between px-2 lg:px-6 py-2">
    <div class="">
      <button class="h-12 w-12 hover:bg-lightblue rounded-full text-3xl text-blue ">
        <i class="fab fa-twitter"></i>
      </button>
      <div>
        <button v-for="tab in tabs" @click="id=tab.id" :key="tab.id" class="flex focus:outline-none mb-3 hover:text-blue items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto" :class="id==tab.id? 'text-blue': '' ">
          <i :class="tab.icon" class="text-2xl mr-4"></i>
          <p class="text-lg hidden lg:block font-semibold text-left">{{tab.title}}</p>
        </button>
      </div>
      <button class="focus:outline-none hover:bg-darkblue  p-3 text-white w-12 h-12 bg-blue lg:h-auto lg:w-full - rounded-full font-semibold">
        <p class="hidden lg:block">Tweet</p>
        <i class="fas fa-plus lg:hidden"></i>
      </button>
    </div>
    <div class="w-full mt-10 relative">
      <button @click="dropdownToggle" class="flex items-center w-full hover:bg-lightblue focus:outline-none rounded-full p-2">
        <img src="./assets/logo.png" class="w-10 h-10 rounded-full" alt="">
        <div class="ml-4 hidden lg:block">
          <p class="text-sm font-bold leading-tight">Fideh YBNL</p>
          <p class="text-sm leading-tight">@defidelity1</p>
        </div>
        <i class="fas fa-angle-down text-lg ml-auto hidden lg:block"></i>
      </button>
      <div v-if="dropdown" class="absolute hi bottom-0 p-3 bg-white left-0 rounded-lg mb-16 shadow-md border-lightest">
        <button @click="dropdown=false" class="flex items-center w-full hover:bg-lightest focus:outline-none p-2">
        <img src="./assets/logo.png" class="w-10 h-10 rounded-full" alt="">
        <div class="ml-4">
          <p class="text-sm font-bold leading-tight">Fideh YBNL</p>
          <p class="text-sm leading-tight">@defidelity1</p>
        </div>
        <i class="fas fa-check text-blue ml-auto"></i>
      </button>
      <button @click="dropdown=false" class="w-full p-3 text-left text-sm focus:outline-none hover:bg-lightest border-top border-lighter">
        Add an Account
      </button>
      <button @click="dropdown=false" class="w-full p-3 text-left text-sm focus:outline-none hover:bg-lightest border-top border-lighter">
        Log out @defidelity1
      </button>
      </div>
    </div>
  </div>
  <!-- Tweet -->
  <div class="w-1/2 h-full overflow-y-scroll">
    <div class="px-5 py-3 border-b border-lighter flex items-center justify-between">
      <h3 class="text-xl font-bold">Home</h3>
      <i class="far fa-star text-xl text-blue"></i>
    </div>
    <div class="px-5 py-3 border-b-8 border-lighter flex">
      <div>
        <img src="./assets/logo.png" class="w-12 h-12 rounded-full" alt="">
      </div>
      <form @submit.prevent="addNewTweet" action="" class="w-full relative px-4">
        <textarea v-model="tweet.content" class="mt-3 pb-3 w-full focus:outline-none" name="" id="" placeholder="What's Up?"></textarea>
        <div class="flex items-center">
          <i class="text-lg text-blue mr-4 far fa-image"></i>
          <i class="text-lg text-blue mr-4 fas fa-file"></i>
          <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
          <i class="text-lg text-blue mr-4 far fa-smile"></i>
        </div>
        <button type="submit" class="h-10 px-4 font-semibold text-white bg-blue rounded-full absolute buttom-0 right-0 hover:bg-darkblue focus:outline-none">
          Tweet
        </button>
      </form>
    </div>
    <div class="flex flex-col-reverse">
        <div v-for="tweet in tweets" :key="tweet" class="w-full p-4 border-b hover:bg-lighter flex">
          <div class="flex-none mr-4">
            <img src="./assets/logo.png" class="h-12 w-12 rounded-full flex-none">
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold"> Steph Dietz </p>
              <p class="text-sm text-dark ml-2"> @SaaSyEth </p>
              <p class="text-sm text-dark ml-2"> 1 sec </p>
              <i class="fas fa-angle-down text-dark ml-auto"></i>
            </div>
            <p class="py-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-comment mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-retweet mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-heart mr-3"></i>
                <p> 1 </p>
              </div>
              <div class="flex items-center text-sm text-dark">
                <i class="fas fa-share-square mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
    <div v-for="follow in following" :key="follow" class="w-full p-4 border-b hover:bg-lighter flex">
      <div class="flex-none mr-4">
        <img src="./assets/logo.png" class="h-12 w-12 rounded-full flex-none" alt="">
      </div>
      <div class="w-full">
        <div class="flex items-center w-full">
          <p class="font-semibold">{{follow.name}}</p>
          <p class="text-sm text-dark ml-2">{{follow.handle}}</p>
          <p class="text-sm text-dark ml-2">{{follow.time}}</p>
          <i class="fas fa-angle-down text-dark ml-auto"></i>
        </div>
        <p class="py-2">
          {{follow.tweet}}
        </p>
        <div class="flex items-center justify-between w-full">
          <div class="flex items-center text-sm text-dark">
            <i class="far fa-comments mr-3"></i>
            <p class="">{{follow.comments}}</p>
          </div>
          <div class="flex items-center text-sm text-dark">
            <i class="fas fa-retweet mr-3"></i>
            <p class="">{{follow.retweets}}</p>
          </div>
          <div class="flex items-center text-sm text-dark">
            <i class="fas fa-heart mr-3"></i>
            <p class="">{{follow.like}}</p>
          </div>
          <div class="flex items-center text-sm text-dark">
            <i class="fas fa-share-squre mr-3"></i>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Trending -->
  <div class="md:block hidden w-1/3 h-full border-l border-lighter py-2 px-6 overflow-y-scroll relative">
  <input type="text" class="rounded-full w-full p-2 pl-12 text-sm bg-lighter" placeholder="Search tweets">
  <i class="fas fa-search left-0 top-0 absolute mt-5 ml-12 text-light text-sm"></i>

  <div class="w-full rounded-lg bg-lightest">
    <div class="flex items-center justify-between p-3">
      <p class="text-lg font-bold">Trends for you</p>
      <i class="fas fa-cog text-lg text-blue"></i>
    </div>
    <button v-for="trend in trending" :key="trend" class="w-full border-t border-lighter flex justify-between hover:bg-lighter p-3">
      <div>
        <p class="text-sm text-left leading-tight text-dark">{{trend.top}}</p>
        <p class="font-bold text-left leading-tight">{{trend.title}}</p>
        <p class="text-left leading-tight text-dark">{{trend.bottom}}</p>
      </div>
      <i class="fas fa-angle-down text-lg text-dark"></i>
    </button>
    <button class="p-3 w-full hover:bg-lighter text-left border-t border-lighter">
      Show more
    </button>
  </div>
  <div class="w-full rounded-lg bg-lightest my-4">
    <div class="flex justify-between p-3">
      <p class="text-lg font-bold">Who to follow</p>
      
    </div>
    <button v-for="friend in friends" :key="friend" class="w-full border-t border-lighter flex hover:bg-lighter p-3">
      <img :src="friend.src" class="w-12 h-12 rounded-full" alt="">
        <div class="ml-4">
          <p class="text-sm font-bold leading-tight">{{friend.name}}</p>
          <p class="text-sm leading-tight">{{friend.handle}}</p>
        </div>
        <button class="text-sm font-blue ml-auto py-2 px-4 rounded-full border-2 border-blue">
          Follow
        </button>
    </button>
    <button class="p-3 w-full hover:bg-lighter text-left border-t border-lighter">
      Show more
    </button>
  </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      dropdown: false,
      tabs: [
        {icon: 'fas fa-home', title: 'Home', id:'home'},
        {icon: 'fas fa-hashtag', title: 'Explore', id: 'explore'},
        {icon: 'far fa-bell', title: 'Notifications', id: 'notifications'},
        {icon: 'far fa-envelope', title: 'Messages', id: 'messages'},
        {icon: 'far fa-bookmark', title: 'Bookmarks', id: 'bookmarks'},
        {icon: 'fas fa-clipboard-list', title: 'Lists', id: 'lists'},
        {icon: 'far fa-user', title: 'Profile', id: 'profile'},
        {icon: 'fas fa-ellipsis-h', title: 'More', id: 'more'}
      ],
      id: '',
      trending: [
        {top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi'},
        {top: 'Music', title: 'We Won', bottom: '135K Tweets'},
        {top: 'Pop', title: 'Blue Ivy', bottom: '40k tweets'},
        {top: 'Trending in US', title: 'Denim Day', bottom: '40k tweets'},
        {top: 'Trending', title: 'When Beyonce', bottom: '25.4k tweets'},
      ],
      friends: [
        {src: './assets/logo.jpg', name: 'Elon Musk', handle: '@teslaBoy'},
        {src: 'monk.jpg', name: 'Adrian Monk', handle: '@detective:)'},
        {src: 'kevin.jpg', name: 'Kevin Hart', handle: '@miniRock'}
      ],
      following: [
        {src: 'elon.jpg', name: 'Elon Musk', handle: '@teslaBoy', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '1,000', retweets: '550', like: '1,000,003'},
        {src: 'kevin.jpg', name: 'Kevin Hart', handle: '@miniRock', time: '55 min', tweet: 'Should me and the rock do another sub-par movie together????', comments: '2,030', retweets: '50', like: '20,003'},
        {src: 'elon.jpg', name: 'Elon Musk', handle: '@teslaBoy', time: '1.4 hr', tweet: 'Haha just made a flame thrower. Shld I sell them?', comments: '100,000', retweets: '1,000,002', like: '5,000,003'},
        {src: 'elon.jpg', name: 'Elon Musk', handle: '@teslaBoy', time: '1.4 hr', tweet: 'Just did something crazyyyyyyy', comments: '100,500', retweets: '1,000,032', like: '5,000,103'}
      ],
      tweets: [
        {content: "It is so nice outside:"}
            ],
      tweet: {content: ""}
    }
  },
  methods: {
    dropdownToggle (){
      this.dropdown = !this.dropdown
    },
    addNewTweet(){
      let newTweet = {
        content: this.tweet.content
      }
      this.tweets.push(newTweet)
    }
  }
}
</script>

<style>
/* npm uninstall tailwindcss postcss autoprefixer */
/* npm install tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9 */
</style>
