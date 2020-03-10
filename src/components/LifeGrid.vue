<template>
  <div>
    <button v-on:click='nextGen'>Next Generation</button>
    <svg id="grid" height=85vh width=85vh>  
      <g v-for="(row,rowIndex) in mainArr" :key="rowIndex">
        <rect 
          v-for="(col,colIndex) in row" :key="colIndex"
          :x=10*colIndex
          :y=10*rowIndex
          :width=10
          :height=10
          stroke=black
          :fill="[col<0.25 ? 'black' : 'white']">
        </rect>
      </g>
    </svg>
  </div>
</template>
  
<script>
export default {
  data: function() {
    return {
      mainArr: this.generateData(50,50)
    }
  },
  methods: {
    generateData(x,y){
      let outArr = []
      for (let index = 0; index < y; index++) {
        let xArr = []
        for (let index2 = 0; index2 < x; index2++) {
          xArr.push(Math.random()) 
        }
        outArr.push(xArr)
      }
      return outArr
    },
    nextGen(){
      let newArr = this.mainArr.map((d,i)=>{
        if (i==0){
          return d.map(x=>x*2)
        }
        else if (i==this.mainArr.length-1){
          return d.map(x=>x*2)
        }
        else {
          return d.map(x=>x*2)
        }
      })
      this.mainArr = newArr
    }
  }
}
</script>

<style>

</style>