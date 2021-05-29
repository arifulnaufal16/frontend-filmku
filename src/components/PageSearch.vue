<template>
<div class="container">
        <div class="container d-flex justify-content-center">
            <div>FILMKU</div>
            <div style="width: 25%"></div>
            <b-form-input v-model="text" placeholder="Search Film"></b-form-input>
        </div>
        <hr>
        <div class="container d-flex">
          <div class="row">
            <div v-for="item in 10" :key="item.id" class="w-25">
                    <div>
                      <b-card
                        title="Card Title"
                        img-src="https://picsum.photos/600/300/?image=25"
                        img-alt="Image"
                        img-top
                        tag="article"
                        style="max-width: 20rem;"
                        class="mb-2"
                      >
                        <b-card-text>
                          Some quick example text to build on the card title and make up the bulk of the card's content.
                        </b-card-text>
                      </b-card>
                    </div>     
            </div>
          </div>
      </div>

</div>
</template>

<style scoped>
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
      search: null
    };
  },
 
  created() {
    this.getProducts();
    
  },
  
 
  methods: {
    // Get All Products
    async getProducts() {
      try {
        const response = await axios.get("http://localhost:5000/api/filmku");
        this.items = response.data.data;
        console.log(this.items)

      } catch (err) {
        console.log(err);
      }
    },
    // Delete Product
  },
  computed: {
    filteredSheeps: function() {
      let searchTerm = (this.search || "").toLowerCase()
      return this.items.filter(function(item) {
        let id = (item.id || "").toLowerCase() 
        let titel = (item.titel || "").toLowerCase() 
        let actor = (item.actor || "").toLowerCase() 
        return id.indexOf(searchTerm) > -1 || titel.indexOf(searchTerm) > -1 || actor.indexOf(searchTerm) > -1 
      })
    }
  },
    
};

</script>