<template>
   <div>
       <div v-for="(value,key) in obj2" :key="key">
          <p class="a1" :id="key"><span>{{key}}</span></p>  
          <!-- 这里是锚点链接，锚点猫的是id，既这里的key，是唯一的，在这里ABC -->
          <dl v-for="(item,index) in value" :key="index" >
            <dt>
               <img  v-lazy="item.CoverPhoto" alt="">
            </dt>
            <dd>
              {{item.Name}}
            </dd>
          </dl>

       </div>
       <!-- 右边定位 -->
         <div class="b3">
           <div v-for="(value,key1) in obj2" :key="key1" >
          <p><a :href="'#'+key1">{{key1}}</a></p>

          </div>
         </div>
         

   </div>
</template>

<script>
export default {
   data(){
      return {
        arr:[],
        obj2:{}
      }
   },

   created (){
      this.axios.get('https://baojia.chelun.com/v2-car-getMasterBrandList.html').then(res=>{
            this.arr=res.data.data;
            this.fn()

      })
   },
   methods:{
     fn(){//处理数据
         let obj={}
          this.arr.map((item)=>{
            if(!obj[item.Spelling.slice(0,1)]){
               obj[item.Spelling.slice(0,1)] =[item]
            }else{
               obj[item.Spelling.slice(0,1)].push(item)
            }
          })
          this.obj2=obj
     }
   }
}
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;
  text-decoration: none;

}
html,body{
  width: 100%;
}
   dl{
     display: flex;
     align-items: center;
     border-bottom: 1px solid #ccc;
     margin-top:5px; 
     
   }
   dt>img{
     width: 40px;
     height: 40px;

   }
  
   .a1{
     width: 100%;
     height: 40px;
     background: #ccc;
     line-height: 40px
   }
   .a1 span{
     margin-left: 10px
   }
   .b3{
   position: fixed;
    top: 30%;
    left: 95%;
   }
  a{
    color: #333
  }
</style>