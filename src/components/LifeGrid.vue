<template>
  <div>
    <button v-on:click='startSim'>Start</button>
    <svg id="grid" height=85vh width=85vh>  
      <g v-for="(row,rowIndex) in mainArr" :key="rowIndex">
        <rect 
          v-for="(col,colIndex) in row" :key="colIndex"
          :x=10*colIndex
          :y=10*rowIndex
          :width=10
          :height=10
          stroke=black
          :fill="[col==1 ? 'black' : 'white']">
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
          xArr.push(Math.random()<0.1 ? 1 : 0) 
        }
        outArr.push(xArr)
      }
      return outArr
    },
    startSim(){
      let interval = setInterval(this.nextGen,2000)
      return interval
    },
    nextGen(){
      let newArr = this.mainArr.map((d,i)=>{
        if (i==0){
          return d.map((x,xi)=>{
            let neighbors = d[xi-1]+d[xi+1]+this.mainArr[i+1][xi-1]+this.mainArr[i+1][xi]+this.mainArr[i+1][xi+1]
            let alive
            if (x==1) {
              neighbors == 2 | neighbors == 3 ? alive = 1 : alive = 0
            }
            else if (x==0) {
              neighbors == 3 ? alive = 1 : alive = 0
            }
            return alive
          })
        }
        else if (i==this.mainArr.length-1){
          return d.map((x,xi)=>{
            let neighbors = d[xi-1]+d[xi+1]+this.mainArr[i-1][xi-1]+this.mainArr[i-1][xi]+this.mainArr[i-1][xi+1]
            let alive
            if (x==1) {
              neighbors == 2 | neighbors == 3 ? alive = 1 : alive = 0
            }
            else if (x==0) {
              neighbors == 3 ? alive = 1 : alive = 0
            }
            return alive
          })
        }
        else {
          return d.map((x,xi)=>{
            let neighbors = d[xi-1]+d[xi+1]+this.mainArr[i-1][xi-1]+this.mainArr[i-1][xi]+this.mainArr[i-1][xi+1]+this.mainArr[i+1][xi-1]+this.mainArr[i+1][xi]+this.mainArr[i+1][xi+1]
            let alive
            if (x==1) {
              neighbors == 2 | neighbors == 3 ? alive = 1 : alive = 0
            }
            else if (x==0) {
              neighbors == 3 ? alive = 1 : alive = 0
            }
            return alive
          })
        }
      })
      this.mainArr = newArr
    }
  }
}
</script>

<style>

</style>