<template>
    <div class="container is-widescreen">
     
      <section class="section" id="app">
        <div class="content">
          <!-- <div class="columns"> -->
            <center><h1>{{nameSubject}}</h1></center>
            <div class="column is-6 " style="margin-left:25%; " >
              <div v-for="subjectnews in selectnews_subject" :key="subjectnews.id" class="card mb-3 ">
                <div  :style="{'background-color':subjectnews.bgSuccess?'#2B3467':'#BAD7E9'}">
                
                <div class="card-content ">
                 
                 
                  <h4  style="color:#FFF;"> 
                    <span class="icon" v-if="!subjectnews.bgSuccess">
                        <i class="fa fa-circle"></i>
                    </span>
                    <span class="icon" v-if="subjectnews.bgSuccess">
                        <i class="fa fa-check-circle"></i>
                    </span>
                    {{subjectnews.topic}}</h4>
                  <h6 style="color:#FFF;margin-bottom:10px">โดย : {{teaachSubject}}</h6>
                  
                  <div style="color:#FFF">วันที่: {{subjectnews.date +"  เวลา: "+ subjectnews.time+" น."}}<span style="float:right"><div class="button" @click="showDetail(subjectnews.id)">ดูเพิ่มเติม > </div></span></div>
                
                </div></div>
                 
                  
                
              </div>
            </div>
          <!-- </div> -->
        </div>
    
  
         <!-- Modal Show DetailSubject -Start -->
        <div class="modal" :class="{'is-active': modalShowDetail}" >
          <div class="modal-background"></div>
          <div class="modal-card" v-for="(subjectnews,index) in selectnews" :key="subjectnews.id">
            <header class="modal-card-head">
              <p class="modal-card-title">{{subjectnews.topic}}</p>
              <button class="delete" aria-label="close" @click=" modalShowDetail=false"></button>
            </header>
            <section class="modal-card-body">
              <!-- Content ... -->
             
             
              <div class="columns" style="margin-bottom: 20px;">
                <h1>รายละเอียดราย : {{subjectnews.detail}}</h1>
              </div>
               <div class="columns" style="margin-bottom: 20px;">
                <div>อาจารย์ผู้สอน : {{teaachSubject}}</div>
              </div>
               <div class="columns" style="margin-bottom: 20px;">
                <div>วันที่ : {{ subjectnews.date }}</div>
              </div>
              
               <div class="columns" style="margin-bottom: 20px;"> 
                <div>เวลา : {{ subjectnews.time }} </div>
              </div>
              
              <div v-if="!subjectnews.bgSuccess" class="button" @click="confirmNews(index)" > ยืนยันทราบข่าวสาร </div>
              
            </section>
            
          </div>
        </div>
        <!-- Modal Add -End -->
      </section>
        
    </div>
  
   
  </template>
  
  <script>
  import axios from "axios";
  // @ is an alias to /src
  export default {
    name: "newsofsubject",
    // props: ['user'],
    data() {
      return {
        selectnews_subject:[],
        newsTotal:[
            {id:1,idSubject:"06016310",teach:"รศ.ดร.นพพร โชติกกำธร",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"20/11/65",time:"8.45",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนเวลาที่ทำการเรียนการสอนเป็น 14.30-16.30 น.",bgSuccess:false},
            {id:2,idSubject:"06016310",teach:"รศ.ดร.นพพร โชติกกำธร",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"12/11/65",time:"10.05",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนสถานที่ที่ทำการสอนเป็น project base 3",bgSuccess:true},
            {id:3,idSubject:"06016325",teach:"ผศ.ดร. ธราวิเชษฐ์ ธิติจรูญโรจน์",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"20/11/65",time:"7.00",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนเวลาที่ทำการเรียนการสอนเป็น 14.30-16.30 น.",bgSuccess:false},


        ],
        modalShowDetail:false,
        nameSubject:this.$route.params.name,
        teaachSubject:this.$route.params.teach,
        idSubject:this.$route.params.idSubject,
        selectnews:[],
        
        
    
  
      };
    },
    mounted() {
        this.showNewSelectSubject();
    },
    methods: {
      confirmNews(index){
        this.modalShowDetail =false
        console.log(index)
        this.newsTotal[index].bgSuccess = true

        
      },
      showDetail(id){
        this.modalShowDetail = true;
        this.selectnews = this.newsTotal.filter((val)=>(val.id==id))
       
      },
      showNewSelectSubject(){
        this.selectnews_subject = this.newsTotal.filter((val)=>val.idSubject==this.idSubject)
      }
    },
  };
  </script>
  