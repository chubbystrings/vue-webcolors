<template>
<transition name="slide" appear mode="out-in">
    <div class="colorApp" >
        <span>HEX:</span> <br>
        <h2 @click.stop.prevent="copyText('hex')"> {{color[0].hex}}</h2> 
        <input id="hex" type="hidden" :value="color[0].hex"> 
         
         <span>RGB:</span> <br>
        <h2 @click.stop.prevent="copyText('rgb')"> {{color[0].rgb}}</h2> 
        <input id="rgb" type="hidden" :value="color[0].rgb"> 
        
        <span>NAME:</span> <br>
        <h2 @click.stop.prevent="copyText('name')"> {{color[0].name}}</h2> 
        <input id="name" type="hidden" :value="color[0].name"> 

        <transition name="copy">
            <p id="copied" v-show="copied">{{copied}}</p>
        </transition>
        
            <div class="displayColorDiv">
            
                <div class="displayColor" :style="{backgroundColor: color[0].hex}"></div>
                
            </div>
       
    
        
        <div class="homeButtonDiv">
        <button @click="backToHome">Home</button>
        </div>
        
    </div>
</transition>    
</template>
<script>
export default {
    data(){
        return {
            copied: ''
        }
    },
    props: ['color'],

    methods: {
        backToHome(){
            this.$emit('home',)
        },

        copyText(value){
            let selected = document.querySelector('#'+ value)
            selected.setAttribute('type', 'text')
            selected.select()
             
            const success = document.execCommand('copy');
            const copy = success ? 'Copied successful' : 'unsuccessful';
            this.copiedTimer(copy)
             

          /* unselect the range */
          selected.setAttribute('type', 'hidden')
          window.getSelection().removeAllRanges()

        },


        copiedTimer(v){
            this.copied = v
            setTimeout(() => {
                this.copied = ''
            }, 2000)
        }
    }
}
</script>
<style scoped>

.colorApp input {
    margin: 0 auto;
    height: 3rem;
    width: 10rem;
    background-color: #2F4F4F;
    border: 1px solid #2F4F4F;
    color: white;
    font-size: 20px;
    text-align: center;
    font-family: inherit;

}



#copied {
    
    margin: 0 auto;
    background-color: lightgreen;
    height: 2rem;
    width: 20rem;
    border-radius: 10px;
    text-align: center;
    color: white;
    padding: auto;
}

h2 {
    
    font: inherit;
    margin: 0.2rem auto;
    font-size: 20px;
    height: 2rem;
    width: 15rem;
}

h2:hover {
   background-color: transparent;
  cursor: pointer;
  box-shadow: 0 0.4rem 1.4rem 0 black;
  transform: translateY(-0.1rem);
  transition: transform 500ms;
  color: black 
    
}

.copyBtn {
    position: absolute;
    right: 1rem;
    border: 1px solid #4AAE9B;
    box-sizing: border-box;
    color: black;
    padding: 2px 5px;
    font: inherit;
    cursor: pointer;
    background-color: #f8f9fa;
    font-size: 15px;
    box-shadow: 1px 1px 1px black;
}

.copyBtn:hover,
.copyBtn:active {
    background-color: #4AAE9B;
    color: black;
}


.displayColorDiv {
  width: 100%;
  position: fixed;
  margin-top: 2rem;
  box-sizing: border-box;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
    
}

.displayColor {
  margin:0 auto;
  height: 4rem;
  width: 17rem;
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

.copy-enter {
  opacity: 0
}
.copy-enter-active {
  transition: opacity 1s;
}


.copy-leave-active {
  animation: slide-out 200ms ease-out forwards; 
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

@media(min-width: 800px){
    .copyBtn {
        right: 30rem;
    }
}

</style>