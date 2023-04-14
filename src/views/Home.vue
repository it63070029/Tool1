<template>
  <div class="container is-widescreen">
    <section class="hero">
      <div class="hero-body">
        <!-- Searchhh -->
        <div class="columns">
          <div class="column is-3"></div>
          <div class="column is-5">
            <input class="input" type="text"  placeholder="Search" v-model="search"/>
          </div>
          <div class="column is-2">
            <button  class="button" @click="showSeach">Search</button>
          </div>
          <div class="column is-3">
            <button class="button" @click="modalAddSubject=true">เพิ่มรายวิชา</button>
          </div>
        </div>
         <!-- Searchhh -->
      </div>
    </section>
    <section class="section" id="app">
      <div class="content">
        <!-- <div class="columns"> -->
          
          <div class="column is-6 " style="margin-left:25%; " >
            <div v-for="mySubject in showMySubject" :key="mySubject.id" class="card mb-3 py-2" style="background-color: #3C486B;">
              
              <div class="card-content ">
               
               
                <h4  style="color:#FFF;">{{mySubject.id}}</h4>
                <h5 style="color:#FFF;">{{mySubject.name}}</h5>
                <div style="color:#FFF">{{mySubject.date +"  "+mySubject.time}}<span style="float:right"><div class="button" @click="showDetail(mySubject.id)">ดูเพิ่มเติม > </div></span></div>
                <!-- <div class="content" style="height: 100px;">descript: {{ shortContent(novel.descript) }}</div> -->
              </div>
               
                
              
            </div>
          </div>
        <!-- </div> -->
      </div>
      <!-- Modal Add -Start -->
      <div class="modal" :class="{'is-active': modalAddSubject}">
        <div class="modal-background"></div>
        <div class="modal-card">
          <header class="modal-card-head">
            <p class="modal-card-title">เพิ่มรายวิชา</p>
            <button class="delete" aria-label="close" @click=" modalAddSubject=false"></button>
          </header>
          <section class="modal-card-body">
            <!-- Content ... -->
            <div class="columns">
              <!-- <div>รหัสวิชา :</div> -->
            </div>
            <div class="columns" style="margin-bottom: 20px;">
              <div class="px-2">รหัสวิชา :</div>
              <!-- <input type="text" class="input" v-model="idSubject"> -->
              <div class="select">
                <select v-model="idSubject" class="px-5 mr-3" style="padding-right:100px">
                  <option v-for="subject in subject" :key="subject.id"  style="padding-right:100px">{{subject.id}}</option>
                </select>
                
              </div>
              <div v-if="idSubject!==''">
              เซค :
               <div class="select">
                <select v-model="idSubject" class="px-5 mr-3" style="padding-right:100px">
                  <option v-for="subject in subject" :key="subject.id"  style="padding-right:100px">{{subject.id}}</option>
                </select>
                
              </div></div>

            </div>
             
            <div class="columns" v-for="subject in subject" :key="subject.id">
              
             <div v-if="idSubject== subject.id">
              <div>รหัสวิชา : {{subject.id}} ชื่อวิชา :{{subject.name}} เวลา : {{subject.time[0].no1}}</div>
              
             </div>
             
            </div>
          </section>
          <footer class="modal-card-foot">
            <button class="button is-success" @click="addMySubject">Add</button>
            <button class="button" @click=" modalAddSubject=false">Cancel</button>
          </footer>
        </div>
      </div>
      <!-- Modal Add -End -->

       <!-- Modal Show DetailSubject -Start -->
      <div class="modal" :class="{'is-active': modalShowDetail}" >
        <div class="modal-background"></div>
        <div class="modal-card" v-for="selectSubject in selectSubject" :key="selectSubject.id">
          <header class="modal-card-head">
            <p class="modal-card-title">{{selectSubject.name}}</p>
            <button class="delete" aria-label="close" @click=" modalShowDetail=false"></button>
          </header>
          <section class="modal-card-body">
            <!-- Content ... -->
           
            <div class="columns" style="margin-bottom: 20px;">
              <h3>รายละเอียดรายวิชา</h3>
            </div>
            <div class="columns" style="margin-bottom: 20px;">
              <div>รหัสวิชา : {{selectSubject.id}}</div>
            </div>
             <div class="columns" style="margin-bottom: 20px;">
              <div>อาจารย์ผู้สอน : {{selectSubject.teach}}</div>
            </div>
             <div class="columns" style="margin-bottom: 20px;">
              <div>ช่องทางติดต่อ</div>
            </div>
            
             <div class="columns" style="margin-bottom: 20px;"> 
              <p>วัน-เวลาที่เรียน : </p>
              <div>{{"  "+selectSubject.date + "  " +selectSubject.time}}</div>
            
            </div>
             <div class="columns" style="margin-bottom: 20px;">
              <div>สถานที่เรียน : {{selectSubject.room}}</div>
            </div>
             
            
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
  name: "Home",
  // props: ['user'],
  data() {
    return {
      
      subject: [
        {id:"06016327",name:"Software",credit:"3",teach:"รศ.ดร.นพพร โชติกกำธร",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"จ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg"}],route:"https://g.page/ITKMITL?share"},
        {id:"90304004",name:"REPORT WRITING",credit:"3",teach:"รศ.ดร.นพพร โชติกกำธร",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"พ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg"}],route:"https://g.page/ITKMITL?share"},
        {id:"06016310",name:"HUMAN INTERFACE DESIGN",credit:"3",teach:"รศ.ดร.นพพร โชติกกำธร",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"จ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg"}],route:"https://g.page/ITKMITL?share"},
      ],
      users:this.user,
      mySubject:[
         {id:"06016310",name:"HUMAN INTERFACE DESIGN",credit:"3",teach:"รศ.ดร.นพพร โชติกกำธร",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"จ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg"}],route:"https://g.page/ITKMITL?share"},
     
        ],
      idSubject:"",
      modalAddSubject:false,
      modalShowDetail:false,
      selectSubject:[],
      search:"",
      showMySubject:[],

    };
  },
  mounted() {
    // this.getNovels();
    // this.getShelfBooks();
    this.showSeach();
  },
  methods: {
    // getNovels() {
    //   axios
    //     .get("http://localhost:3000", {
    //       params: {
    //         search: this.search,
    //       },
    //     })
    //     .then((response) => {
    //       this.novels = response.data;
    //     })
    //     .catch((err) => {
    //       console.log(err);
    //     });
    // },
    // imagePath(file_path) {
    //   if (file_path) {
    //     return "http://localhost:3000/" + file_path;
    //   } else {
    //     return "https://bulma.io/images/placeholders/640x360.png";
    //   }
    // },
  
    addMySubject(){
      console.log("AddSubject")
      // for(let i =0;i<this.mySubject.length;i++){
      //   if(this.idSubject==this.mySubject[i].id){
      //     alert("คุณได้เพิ่มวิชานี้ในชั้นเรียนแล้ว")
      //   }
        
      //   else{
      //     console.log("hiii")
      //     let addS = this.subject.filter(val.id ==this.idSubject)
      //      console.log(addS)
      //     this.mySubject.push(addS);
      //     this.modalAddSubject = false
      //   }

      // }
      let addS = this.subject.filter((val)=>(val.id ==this.idSubject))
      let myS = this.mySubject.filter((val)=>(this.idSubject ==val.id))
      console.log(addS[0])
      console.log(myS)
      if(this.idSubject!==""){

        if(myS.length<=0){
          this.mySubject.push(addS[0]);
          this.showMySubject = this.mySubject
          this.modalAddSubject = false;
        }
        else{
          alert("คุณได้เพิ่มวิชานี้ในชั้นเรียนแล้ว")
        }
      }
      else{
        this.modalAddSubject = false
      }
      

      
    },
    showDetail(id){
      this.modalShowDetail = true;
      this.selectSubject = this.mySubject.filter((val)=>(id==val.id))
    },
    showSeach(){
      if(this.search==''){
        this.showMySubject=this.mySubject
      }
      else{
        this.showMySubject=this.mySubject.filter((val)=>(val.id==this.search || val.name ==this.search))
      }
    }
  },
};
</script>
