<template>
    <div class="home" v-if="arr" >
          <div v-for="(item,index) in arr" :key="index">
             <h4>{{item.letter}}</h4>
             <div v-for="(item1,index1) in item.children" :key="index1" class="item"><img :src=item1.CoverPhoto alt="">{{item1.Name}}</div>
          </div>
          <div class="right"><li v-for="(item,index) in arr" :key="index" @click="fun()">{{item.letter}}></div>

    </div>
</template>

<script>
export default {
   data(){
      return {
        arr:[]
      }
   },
   methods:{
      fun(){
         
      }
   },
   created (){
      this.$http.get('https://baojia.chelun.com/v2-car-getMasterBrandList.html').then(res=>{
        if(res.data.code == 1){
           res.data.data.map((item,index)=>{
              var letter = item.Spelling[0];
              var newArr = res.data.data.filter(item => item.Spelling[0] == letter)

              if(this.arr.findIndex(item => item.letter == letter) === -1){
                  this.arr.push({letter,children:newArr})
              }
           })
            console.log(letter==newArr)
              

        }else{
           alert(res.data.msg)
        }
      })
   }
}
</script>

<style scoped>
.home {
  width: 100%;
  height: 100%;
}
.wrap{
  width: 100%;
  height: 100%;

}
.right{
  position: fixed;
  display: flex;
  flex-direction: column;
  right: 15px;
  top: 120px;

}
.home h4{
  width: 100%;
  height: 28px;
  background: #ccc;
  line-height: 28px;
}
.home .item img{
   width: 30px;
   margin: 5px;
}
.home .item{
  width: 100%;
  height: 45px;
  line-height: 45px;
  padding:  0 10px;
}
</style>