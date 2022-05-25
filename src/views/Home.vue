<template>
<div>
  <top />

</div>
 
</template>

<script>
// @ is an alias to /src

import top from '../components/top'

export default {
  components:{
    top,
    
  },
  filters:{
    
  },
  name: 'Home',
  created(){
  
  },
  mounted(){
  
  },
  data(){
    return{

    }
  },
  methods:{
   
  },
  watch:{
      
  },
 
}
 
</script>
<style lang="less" scoped>
.top_file{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.file_box{
  padding: 20px;
}
.file_setting{
}
.file_box_set{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.box_check{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
