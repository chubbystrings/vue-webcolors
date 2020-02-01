<template>
    <div class="displayedColorsDiv">
        <div class="displayedColors" @click="clicked(v)">{{v}}
             <span class="sampleColor" :style="{backgroundColor: v}"></span>
        </div>
    </div>
</template>
<script>
export default {
    props: ['v'],

    methods: {
        clicked(key){
            this.$emit('clicked', key)
        }
    }
}
</script>
<style scoped>
.displayedColors {
    margin-top: 0.7rem;
  font-size: 20px;
  height: 3.0rem;
  width: 16rem;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  
}

.displayedColors:hover {
  background-color: transparent;
  cursor: pointer;
  box-shadow: 0 0.4rem 1.4rem 0 black;
  transform: translateY(-0.1rem);
  transition: transform 500ms;
  
}

span.sampleColor {
  width: 7rem;
  height: 2rem;
  border-radius: 20px;
  position: absolute;
  left: 17rem;;
  
}

.displayedColors {

    font-size: 1.6rem;
    box-sizing: border-box;
    padding: 0.5rem;
}
</style>