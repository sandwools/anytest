<template>

  <div class="month">
       <div class="background">
       </div>

        <!-- 背景图 -->
          <img
            class="ss"
            src="../assets/ss.png"
          />
          <!-- 背景图 -->

        <div class="back_button">
          <back_button></back_button>
        </div>

        <div class="layer2_1 flex-row">
          <span class="txt2">请选择</span>
        </div>



        <div id="fin_chose_box">

           <div class="fin_chose">
              <div class="fin_img">
                 <img
                   src="../assets/food_0.png"
                 />
                 </div>

                 <div class="fin_dis">
                   {{$store.state.randomFood_1}}<br>
                   {{$store.state.randomFood_1_2}}<br>
                   {{$store.state.randomFood_1_3}}<br>
                 </div>

                 <div class="fin_check">
                 <input type="radio" name="check" v-model="isFirst" value=1 />
                 </div>   
             </div>

             <div class="fin_chose">
              <div class="fin_img">
                 <img
                   src="../assets/food_0.png"
                 />
                 </div>

                 <div class="fin_dis">
                   {{$store.state.randomFood_2}}<br>
                   {{$store.state.randomFood_2_2}}<br>
                   {{$store.state.randomFood_2_3}}<br>
                 </div>

                 <div class="fin_check">
                 <input type="radio" name="check" v-model="isSecond" value=2 />
                 </div>   
             </div>

             <div class="fin_chose">
              <div class="fin_img">
                 <img
                   src="../assets/food_0.png"
                 />
                 </div>

                 <div class="fin_dis">
                   {{$store.state.randomFood_3}}<br>
                   {{$store.state.randomFood_3_2}}<br>
                   {{$store.state.randomFood_3_3}}<br>
                 </div>

                 <div class="fin_check">
                 <input type="radio" name="check" v-model="isThird" value=3 />
                 </div>   
             </div>
       </div>


<!-- button -->

        
          <div id="button-div">

          <div class="button-down">
          <button class="month-button" @click="toFin">&nbsp;&nbsp;&nbsp;就它了&nbsp; &nbsp;&nbsp;</button>
          </div>
          
          <div class="button-down">
          <button class="month-button" @click="f5">&nbsp;&nbsp;&nbsp;换一波&nbsp; &nbsp;&nbsp;</button>
          </div>
          </div>
      
    
  </div>
</template>

<script>
import back_button from '@/components/back_button'
import Axios from "axios";
//import Axios from "axios";

export default {
  name: 'result',
  components: {
      back_button,
  },
  methods:{
    f5(){
      this.$router.push("/range");
      this.$store.commit("rest");
    },
    toFin(){
      //console.log(this.isThird);
      if(this.isThird===0&&this.isFirst===0&&this.isSecond===0)
      {
        alert("欸嘿，请选择哦");
      }
      else{
      if(this.isFirst!==0){this.$store.commit("first");
        this.$store.state.id=this.$store.state.randomFood_1_id}
      if(this.isSecond!==0){this.$store.commit("second");
        this.$store.state.id=this.$store.state.randomFood_2_id}
      if(this.isThird!==0){this.$store.commit("third");
        this.$store.state.id=this.$store.state.randomFood_3_id}
      this.$router.push("/result");

        Axios({
          url:'http://150.158.143.166:8080/SchM/id',
          params: {
            id: this.$store.state.id,
          },
        }).then(res => {
          let ran1=res.data.toString();
          let food=[];

          if(ran1===""){
            alert("欸嘿，没有符合筛选条件的捏🥰")
            this.$router.push("/home");
          }

          for(let i=0;i<15;i++){
            let index;
            index=ran1.indexOf("\n");
            food[i]=ran1.slice(0,index);
            ran1=ran1.slice(index+1);

            this.$store.state.hot=food[0];
            this.$store.state.hot2=food[1];
            this.$store.state.hot2=food[2];

          }
        });
    }
    },
  },

  data(){
   return{
     chose_1: this.$store.state.randomFood_1,
     isFirst: 0,
     isSecond: 0,
     isThird: 0,
   }
  }
}
</script>


<style>
.fin_dis{
margin-top: 10%;
width: 50%;
height: 200%;
text-align: center;
}

.fin_check{
width: 20%;
display: flex;
}

.fin_check>input{
margin-top:60%;
margin-left:30%;
}

.fin_img>img{
width: 100%;
height: 100%;
}

.fin_img{
width: 30%;
}

.fin_chose{
display: flex;
width: 100%;
height: 10%;
border: 3px solid blue;
border-radius: 7px;
padding: 10px;
margin-top:10px;
}

</style>

<style>
.background {
  height: 100%;
  background: url(../assets/bg2.png) -0.19vw
    0vw no-repeat;
  background-size: 100% 100%;
  width: 100%;
  left: 0;
  top: 1.58vw;
  z-index:-99;
  position: absolute;
  
}

.back_button{
  width: 7.78vw;
  height: 7.78vw;
  margin: 6.01vw 0 0 7.68vw;
  
}


.layer2_1 {
  width: 44.17vw;
  height: 7.13vw;
  margin: 25px 50px 25px 100px;
}

.txt2 {
  width: 44.17vw;
  height: 7.13vw;
  overflow-wrap: break-word;
  color: rgba(0, 0, 0, 1);
  font-size: 7.22vw;
  font-family: STSong;
  text-align: center;
  white-space: nowrap;
  line-height: 7.23vw;
  display: block;
  
}


.ss {
  width: 50%;
  height: 45.5vw;
  margin-top: 130%;
  margin-left: 40%;
  
  z-index:-99;
  position: absolute;
}



#button-div{
  display: flex;
  justify-content: space-between;
  
  margin:5%;

}

.button-down{
  margin:10%;
  width: 30%;
  height: 10%;
  text-align: center;
}

.month-button {
	box-shadow:inset 0px 10px 16px -9px #bbdaf7;
  background: #79bbff linear-gradient(to bottom, #79bbff 5%, #378de5 100%);
  border-radius:6px;
	border:1px solid #84bbf3;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:8px;
	font-weight:bold;
	padding:8px 9px;
	text-decoration:none;
	text-shadow:-1px 0px 14px #528ecc;
}
.month-button:hover {
  background: #378de5 linear-gradient(to bottom, #378de5 5%, #79bbff 100%);
}
.month-button:active {
	position:relative;
	top:1px;
}
</style>
