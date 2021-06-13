<template>
<div class="container"  >
        <div class="container d-flex justify-content-center">
            <div>
                <h1>FILMKU</h1>
            </div>
            <div style="width: 25%"></div>
            <b-form-input v-model="search"  placeholder="Search Film"></b-form-input>
            <!-- <b-icon icon="exclamation-circle-fill" variant="info" style="width: 60px; height: 60px;" data-toggle="popover" title="Popover title" data-content="And here's some amazing content. It's very engaging. Right?"></b-icon> -->
            <!-- <button type="button" class="btn btn-lg btn-danger rounded-circle" ></button> -->
        </div>
        <hr>
        <div class="container d-flex">
          <div class="row">
            <div v-for="item in resultQuery" :key="item" class="card1">      
                    <div>
                      <b-card
                        :title="item.title + ' (' +  item.releaseYear + ')' "
                        :img-src="item.urlPic"
                        img-alt="Image"
                        img-top
                        tag="article"
                        style="max-width: 20rem;"
                        class="mb-2"
                      >
                        <b-card-text>
                          <h6>
                            Director : {{item.director}}
                          </h6>
                        </b-card-text>
                        <b-card-text>
                        </b-card-text>
                            <b-button  data-id="2" v-b-modal:[`example-modal-${item.id}`] >Click For Detail</b-button>
                            <b-modal :id="`example-modal-${item.id}`" v-model="searchgenre">
                                 <h2>{{item.title}}</h2>
                                <div class="container">
                                    <div class="row">
                                        <div class="col"> 
                                            <img :src="item.urlPic" alt="" style="width: 100%">
                                        </div>
                                        <div class="col">
                                            <p>Director : {{item.director}}</p>
                                            <p>Release Year : {{item.releaseYear}}</p>
                                            <p>Duration : {{item.duration}} minute</p>
                                            <p>Actor : {{item.actor}} </p>  
                                            <p>Actor : {{genre}} </p>  
                                            <div :key="subs" v-for="subs in resultQuery1"> 
                                                <!-- <div v-if="subs.genreID == item.sub"> -->
                                                    <p>{{subs.genreID}}</p> 
                                                <!-- </div> -->
                                            </div>
                                        </div>
                                    </div>
                                    <p>Desc : {{item.description}}</p>
                                </div>
                                <div class="container">
                                </div>
                                <div>
                                </div>
                            </b-modal>
                      </b-card>
                    </div>     
            </div>
          </div>
      </div>

</div>
</template>

<style scoped>
@media (min-width: 761px) {
    .card1{
        width: 250px;
    }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>



<script>
// import axios
import axios from "axios";
export default {
  name: "Content",
  data() {
    return {
        items: [],
        genre: [],
        search: null,
        searchgenre: null,
    };
  },
 
  created() {
    this.getProducts();
    this.getGenreFilm();
  },
  
 
  methods: {
    // Get All Products
    async getProducts() {
      try {
        const response = await axios.get("http://localhost:5000/api/filmku");
        this.items = response.data.data;
        console.log(this.items);

      } catch (err) {
        console.log(err);
      }
    },
    
    async getGenreFilm() {
        try {
        for(var i = 1 ; i <= 30; i++){
            if(i == 4 ){
                continue
            }
            else {
                let x = String
                if(i < 10) {
                    x = "http://example.com/0"+i
                }
                else {
                    x = "http://example.com/"+i
                }
            const response = await axios.get("http://localhost:5000/api/genres?sub="+x);
            this.genre = response.data.data
            // console.log(this.checks)
            }

        }
        // console.log("1")

      } catch (err) {
        console.log(err);
      }
    },


    // Delete Product
  },
  computed: {
    // filteredSheeps: function() {
    //   let searchTerm = (this.search || "").toLowerCase()
    //   return this.items.filter(function(item) {
    //     let title = (item.title || "").toLowerCase() 
    //     let year = (item.releaseYear || "").toLowerCase() 
    //     let duration = (item.duration || "").toLowerCase() 
    //     let director = (item.director || "").toLowerCase() 
    //     let actor = (item.actor || "").toLowerCase() 
    //     return  title.indexOf(searchTerm) > -1 || year.indexOf(searchTerm) > -1 || duration.indexOf(searchTerm) > -1 || director.indexOf(searchTerm) > -1  || actor.indexOf(searchTerm) > -1
    //   })
    // },
    resultQuery(){
      if(this.search){
      return this.items.filter((item)=>{
            let judul = this.search.toLowerCase().split(' ').every(v => item.title.toLowerCase().includes(v))
            let year = this.search.toLowerCase().split(' ').every(v => item.releaseYear.toLowerCase().includes(v))
            let duration = this.search.toLowerCase().split(' ').every(v => item.duration.toLowerCase().includes(v))
            let director = this.search.toLowerCase().split(' ').every(v => item.director.toLowerCase().includes(v))
            let actor = this.search.toLowerCase().split(' ').every(v => item.actor.toLowerCase().includes(v))
        return judul || year || duration || director || actor 
      })
      }else{
        return this.items;
      }
    },
    resultQuery1(){
          if(this.searchgenre){
          return this.items.filter((genre)=>{
                let genres = this.searchgenre.toLowerCase().split(' ').every(v => genre.genreID.toLowerCase().includes(v))
            return genres
          })
          }else{
            return this.items;
          }
        },
      },
    
};



</script>