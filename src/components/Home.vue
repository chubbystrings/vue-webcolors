<template>

<div>
  <!-- <app-color  :color="singleMatched" @home="colorApp = false, pageNumber = 0" v-if="colorApp"></app-color> -->
    <div class="hello input">
      <h1>WebColors</h1>
      
      
      <input @focus="changeScroll" @blur="resetScroll"  type="text" ref="input"  placeholder="search colors e.g: gold, #ffd700, 255">
      <button class="colorSearchBtn" @click="showValue">Search</button>
      <div class="colorOptions" v-if="value">
        
        <transition-group name="fade" appear>
          <app-colors v-for="v in paginatedData" @clicked="clickColor($event)" :key="v" :v="v">{{v}}</app-colors>
        </transition-group>
      </div>
   

      <transition name="fade" appear>
      <div class="paginationBtn" v-if="!windowWidth">
        <div  v-if="value"><em >Page {{pageCount > 0 ? pageNumber + 1 : pageNumber = 0}} of {{pageCount}}</em></div>
        <button :disabled="pageNumber === 0 || value == ''" @click="prevPage">Prev</button>
        <button :disabled="pageNumber >= pageCount - 1 || value == ''" @click="nextPage">Next</button>
        
      </div>
      </transition>
     
    </div>
  </div>
</template>

<script>
import store from '../store/index'
import Color from '../components/Color'
import Colors from '../components/Colors'
import { mapState} from 'vuex'
export default {
  data(){
    return {
      colorSearch: '',
      colorApp: false,
      pageNumber: 0,
      matched: [],
      singleMatched: [],
      loaded: false,
      initialOffset: '',
      windowWidth: false,
      // value: '',
      listData: '',
      size: 7
    }
  },

  props: ['page'],
  
  computed: {
    
    ...mapState(['value']),

    filteredColors(){
      const e = Array.from(this.$store.getters.getValue)[0]

      if(e && e === '#'){
        this.$store.dispatch('alterValue', this.$store.getters.getValue.toUpperCase())
        this.colorSearch = 'hex'
        
      }

      if( e && /^[a-zA-Z]/.test(e)){
        this.$store.dispatch('alterValue', this.$store.getters.getValue.toLowerCase())
        this.colorSearch = 'name'
        
      }

      if(e && Number(e)){
        this.colorSearch = 'rgb'
       
      }

      const matched = []
      
      this.$store.getters.getColors.forEach((color) => {
        if(e && this.colorSearch){
          if(this.colorSearch === 'hex' || this.colorSearch === 'name'){
            matched.push(color[this.colorSearch])
          }
          if(this.colorSearch === "rgb"){
            matched.push(`rgb(${color[this.colorSearch]})`)
          }
        }
          
      })
        
        
      return matched.filter((f) => {
          return f.match(this.$store.getters.getValue)
      })
      
    },

    pageCount(){
      if(this.$store.getters.getValue){
      this.listData = this.filteredColors.map((m) => m)
      let l = this.listData.length, s = this.size
      return Math.ceil(l/s)
      }
    },

    paginatedData(){
      const start = this.pageNumber * this.size, end =  start + this.size
      return this.listData.slice(start, end)
    },


    
  },

  methods: {
    clickColor(v){
      let matcher;
      if(this.colorSearch === 'rgb'){
        matcher = v.match(/\d+/g).join(', ')
        this.$store.dispatch('alterValue', matcher)
        
      }else{
        matcher = v
        this.$store.dispatch('alterValue', matcher)
      }
   
      if(this.singleMatched.length > 0){
        this.singleMatched = []
        this.singleMatched.push(this.$store.getters.getColors.find((color) => color[this.colorSearch] === matcher))
        
      }else{
        this.singleMatched.push(this.$store.getters.getColors.find((color) => color[this.colorSearch] === matcher))
        
      }
      
      this.$emit('matchedColorArray', this.singleMatched)
      this.$emit('showPage')

    },

    showValue(){
      if(!this.$refs.input.value){ return false}
      this.$store.dispatch('alterValue', this.$refs.input.value)
    },
    nextPage(){
        this.pageNumber++
    },
    prevPage(){
        this.pageNumber--
    },

    changeScroll(){
       this.initialOffset = window.innerWidth
       if(this.initialOffset < 600){
        
         this.windowWidth = true
       }
      
    },

    resetScroll(){
      this.windowWidth = false
    }
  },

  components: {
    appColor: Color,
    appColors: Colors
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.input input {
    font: inherit;
    width: 50vw;
    padding: 6px 12px;
    box-sizing: border-box;
    border: 1px solid #ccc;
    border-radius: 20px;
    box-shadow: 1px 2px 2px 0px black;
    height: 2.5rem;
   
  }

  .input input:focus {
    outline: none;
    border: 1px solid #4AAE9B;
    background-color: #eee;
  }

.paginationBtn button {
  border: 1px solid #4AAE9B;
  color: black;
  padding: 10px 20px;
  font: inherit;
  cursor: pointer;
  background-color: #f8f9fa;
} 

.colorSearchBtn {
  margin-left: 1rem;
   border: 1px solid #4AAE9B;
  color: black;
  padding: 10px 20px;
  font: inherit;
  cursor: pointer;
  background-color: #f8f9fa;
}

.colorSearchBtn:hover,
.colorSearchBtn:active {
background-color: #4AAE9B;
color: black;
}

.colorSearchBtn[disabled],
.colorSearchBtn[disabled]:hover,
.colorSearchBtn[disabled]:active {
border: 1px solid #ccc;
background-color: transparent;
color: #ccc;
cursor: not-allowed;
}

.paginationBtn {
  
  width: 100%;
  position: fixed;
  bottom: 1.5rem; 
  height: 4rem;
}

.paginationBtn button:hover,
.paginationBtn button:active {
background-color: #4AAE9B;
color: black;
}

.paginationBtn button[disabled],
.paginationBtn button[disabled]:hover,
.paginationBtn button[disabled]:active {
border: 1px solid #ccc;
background-color: transparent;
color: #ccc;
cursor: not-allowed;
}

.colorOptions {
  
  display: flex;
  justify-content: flex-start;
  text-align: left;
  box-sizing: border-box; 
}


/* .fade-enter {
  opacity: 0
}
.fade-enter-active {
  transition: opacity 1s;
}

.fade-leave {
  
}

.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
  position: absolute;
}

.fade-move {
  transition: transform 1s;
} */

@media (max-width: 800px){
  .paginationBtn {
    width: 96%;
    position: absolute;
  }
}
</style>
