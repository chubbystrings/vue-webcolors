<template>

  <div id="app" :style="{backgroundColor: color}">

     <transition name="slide" appear>
      <Home v-if="colorApp" @showPage="colorApp = false"  @matchedColorArray="singleMatched = $event" :pageNum="page" ></Home>
    </transition>

    <transition name="fade" appear>
      <app-color v-if="!colorApp" :color="singleMatched" @home="colorApp = true" ></app-color>
    </transition>
  
            
  </div>

</template>

<script>
import Home from './components/Home.vue'
import Color from './components/Color.vue'

export default {
  data(){
    return {
      color: '',
      colorApp: true,
      singleMatched: '',
      page: null,
      
    }
  },
  name: 'app',
  components: {
    Home,
    appColor: Color
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
  
}

body {
  background: #2F4F4F
  
}

.fade-enter {
  opacity: 0
}
.fade-enter-active {
  transition: opacity 1s;
}


.fade-leave-active {
  transition: opacity 100ms ease-out forwards;
  opacity: 0

  
}


.slide-enter {
  opacity: 0
}

.slide-enter-active {
  transition: opacity 100ms ease-out forwards;

}

.slide-leave-active {
    animation: slide-out 100ms ease-out forwards;
    opacity: 0;

}

.slide-move {
    transition: transform 3s ease
}



    @keyframes slide-in {
        from {
            transform: translateX(-200px);
            opacity: 0
        }
        to {
            transform: translateX(0);
            opacity: 1
        }
    }
    @keyframes slide-out {
        from {
            transform: translateX(0);
            opacity: 1
        }
        to {
            transform: translateX(-200px);
            opacity: 0;

        }
    }

</style>
