<template>
<transition name="slide" appear mode="out-in">
    <div class="colorApp" >
        <h1> HEX {{color[0].hex}}</h1>
        <h1> RGB {{color[0].rgb}}</h1>
        <h3>{{color[0].name}}</h3>
        
        <transition name="fade" appear>
            <div class="displayColorDiv">
                <div class="displayColor" :style="{backgroundColor: color[0].hex}"></div>  
            </div>
        </transition>
        <transition name="fade" appear>
            <div class="homeButtonDiv">
            <button @click="backToHome">Home</button>
            </div>
        </transition>
    </div>
</transition>    
</template>
<script>
export default {
    props: ['color'],

    methods: {
        backToHome(){
            this.$emit('home', 'back')
        }
    }
}
</script>
<style scoped>


.displayColorDiv {
  width: 100%;
  position: fixed;
  top: 15rem;
}

.displayColor {
  margin:0 auto;
  height: 4rem;
  width: 15rem;
  border-radius: 30px;
  transition: background-color 1s ease-out;
}

.homeButtonDiv {
  width: 100%;
  position: fixed;
  bottom: 3rem;
}

.colorApp button {
    border: 1px solid #4AAE9B;
    box-sizing: border-box;
    color: black;
    padding: 10px 20px;
    font: inherit;
    cursor: pointer;
    background-color: #f8f9fa;

}

.colorApp button:hover,
.colorApp button:active {
    background-color: #4AAE9B;
    color: black;
}

.colorApp button[disabled],
.colorApp button[disabled]:hover,
.colorApp button[disabled]:active {
    border: 1px solid #ccc;
    background-color: transparent;
    color: #ccc;
    cursor: not-allowed;
}

.fade-enter {
  opacity: 0
}
.fade-enter-active {
  transition: opacity 3s;
}

/* .fade-leave {
  
} */

.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
  position: absolute;
}
.fade-move {
  transition: transform 1s;
}

.slide-enter-active {
    animation: slide-in 200ms ease-out forwards
    

}
.slide-leave-active {
    animation: slide-out 200ms ease-out forwards;

}
.slide-move {
    transition: transform 1s ease-out;
}



    @keyframes slide-in {
        from {
            transform: translateY(-30px);
            opacity: 0
        }
        to {
            transform: translateY(0);
            opacity: 1
        }
    }
    @keyframes slide-out {
        from {
            transform: translateY(0);
            opacity: 1
        }
        to {
            transform: translateY(-30px);
            opacity: 0;

        }
    }


</style>