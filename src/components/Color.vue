<template>
<transition name="slide" appear mode="out-in">
    <div class="colorApp" >
        <h2> HEX: {{color[0].hex}}
            <span  class="copyBtn" @click.stop.prevent="copyText('hex')">Copy</span>
        </h2> 
        <input id="hex" type="hidden" :value="color[0].hex"> 
        
         
        <h2> RGB: {{color[0].rgb}}
            <span  class="copyBtn" @click.stop.prevent="copyText('rgb')">Copy</span>
        </h2> 
        <input id="rgb" type="hidden" :value="color[0].rgb"> 
        
        <h2> NAME: {{color[0].name}}
            <span  class="copyBtn" @click.stop.prevent="copyText('name')">Copy</span>
        </h2> 
        <input id="name" type="hidden" :value="color[0].name"> 
         
        
            <p id="copied" v-if="copied">{{copied}}</p>
        
        
        
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
    font-size: 14px;
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

@media(min-width: 800px){
    .copyBtn {
        right: 30rem;
    }
}

</style>