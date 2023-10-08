<template>
  <div id="app">
    <div style="width:1500px;height:800px;display:flex;">
      <fdView ref="fdView" style="flex:0 0 600px;height:600px" @exportChosenNodes="handleExportChosenNodes"></fdView>
      <SequenceView @exportBrushIds="handleExportBrushIds" ref="SequenceView" style="flex:0 0 800px;height:800px;margin:0 0 0 100px;" />
    </div>

    
  </div>
</template>

<script>

import SequenceView from './components/SequenceView/SequenceView.vue'
import fdView from './components/fdView/fdView.vue'

import * as d3 from 'd3';

export default {
  name: 'App',
  components: {
    SequenceView,
    fdView,
  },
  methods:{
    handleExportBrushIds(ids){//序列图刷选
      this.$refs['fdView'].setFilter(ids)
    },
    handleExportChosenNodes(ids){
      this.$refs['SequenceView'].setHighlight(ids);//测试接口
    }
  },
  mounted(){
    d3.json('static/faker_links（序列）.json',(links)=>{
      d3.json('static/faker_nodes（序列）.json',(nodes)=>{
        this.$refs['fdView'].start(nodes,links);
        this.$refs['SequenceView'].start(nodes,links);
      })
    })

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
