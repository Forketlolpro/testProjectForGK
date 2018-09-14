<template>
  <span><a v-for="tag in this.sortTags">{{tag}} </a></span>
</template>

<script>
    export default {
      props:['tags'],
      name: "tagList",
      mounted:function(){
        this.length=this.tags.length;
        this.sortTags=this.tags.map((item, i, arr)=>{
          let tmp =item.split('');
          if (i===arr.length-1){
            tmp.pop();
            tmp.push('.')
          } else {
            tmp.push(',');
          }
            return tmp.join('');
        });
      },
      data(){
        return{
          sortTags:[],
          length:undefined,
        }
      },
    }
</script>

<style scoped>
  a{
    font-size: 13px;
    line-height: 16px;
    color: #666;
  }
a:hover{
  cursor: pointer;
  text-decoration: underline;
}
</style>
