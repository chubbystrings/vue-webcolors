<template>

  <div id="app" :style="{backgroundColor: color}">
    <transition name="slide" mode="out-in" appear>
    <Home @background="color=$event" ></Home>
    </transition>
  </div>

</template>

<script>
import Home from './components/Home.vue'

export default {
  data(){
    return {
      color: ''
    }
  },
  name: 'app',
  components: {
    Home
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

.slide-enter-active {
    animation: slide-in 200ms ease-out forwards
    

}
.slide-leave-active {
    animation: slide-out 100ms ease-out forwards;

}

.slide-move {
    transition: transform 1s ease
}



    @keyframes slide-in {
        from {
            transform: translateX(-30px);
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
            transform: translateX(-30px);
            opacity: 0;

        }
    }

</style>
