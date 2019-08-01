<template>
<div class="home">

   <div class="headerBox">

     <div class="wrap">

   <div class="search" >
     <!-- I had to use svg search icon and custom css here so you know 
I know how to work without using helper libraries like bootstrap and fontawesome :) -->
     <div class="searchIcon"  v-if="showInput">
  <svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve">
<g>
<g>
<path d="M508.875,493.792L353.089,338.005c32.358-35.927,52.245-83.296,52.245-135.339C405.333,90.917,314.417,0,202.667,0
  S0,90.917,0,202.667s90.917,202.667,202.667,202.667c52.043,0,99.411-19.887,135.339-52.245l155.786,155.786
  c2.083,2.083,4.813,3.125,7.542,3.125c2.729,0,5.458-1.042,7.542-3.125C513.042,504.708,513.042,497.958,508.875,493.792z
    M202.667,384c-99.979,0-181.333-81.344-181.333-181.333S102.688,21.333,202.667,21.333S384,102.677,384,202.667
  S302.646,384,202.667,384z"/>
</g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g><g></g>
</svg>

     </div>

     <template  v-if="showInput">
       <input type="text" class="searchTerm" v-model="inputData" @input="getSearchInput" placeholder="Search for photo">
     </template>

      <template  v-if="showSearching">
        <h1>Searching for <span class="searchWord">"Fun"</span></h1>
      </template>

      <template  v-if="showSearchResultText">
        <h1>Search Results for <span class="searchWord">"Fun"</span></h1>
      </template>
      

   </div>

</div>
    </div>

    <div class="cards">
      <Loader v-if="showLoader" />
      <Cards :apiData="apiData" v-else />
    </div>


</div>

</template>


<script>

import Cards from "../components/cards.vue";
import Loader from "../components/loader.vue";
import { setTimeout } from 'timers';
import axios from 'axios';


export default {
    name: 'Home',
    components: {
      'Cards': Cards,
      'Loader': Loader
    },
    data: function () {
      return {
         inputData:null,
         apiData:[],
         showLoader: true,
         showInput: true,
         showSearching: false,
         showSearchResultText: false

      }
      
    },

    methods: {
      searchPhotos(searchTerm) {
        axios.get(`https://api.unsplash.com/search/photos?page=1&query=${searchTerm}&per_page=7&client_id=d0ebc52e406b1ac89f78ab30e1f6112338d663ef349501d65fb2f380e4987e9e`)
        .then(res => {
          let $results = res.data.results.slice(0,7);
          let filteredResults = $results.map( item => {
            return {
              id: item.id,
              author: item.user.name,
              title: item.description,
              picture: item.urls.raw
            }
          });
          this.apiData = this.apiData.splice(0,7,filteredResults);
          console.log(filteredResults);
        })
        .catch(err => console.log(err));
      },

      getSearchInput() {
        this.searchPhotos(this.inputData);
      },

      initialQuery() {
      axios.get(`https://api.unsplash.com/search/photos?page=1&query=fun&per_page=7&client_id=d0ebc52e406b1ac89f78ab30e1f6112338d663ef349501d65fb2f380e4987e9e`)
      .then(res => {
        let $results = res.data.results.slice(0,7);
        let filteredResults = $results.map( item => {
          return {
            id: item.id,
            author: item.user.name,
            title: item.description,
            picture: item.urls.raw
          }
        });
        this.apiData = filteredResults;
        console.log(filteredResults);
      })
      .catch(err => console.log(err));

      }

    },

    mounted: function () {
        setTimeout(() => this.showLoader = false, 2000);
        this.initialQuery();
        if ( !this.apiData.length && this.inputData) {
          this.showInput = false;
          this.showSearching = true;
          this.showLoader = true;
        } 
        else if (this.apiData && this.inputData) {
          this.showLoader = false;
          this.showSearching = false;
          this.showSearchResultText = true;
        } else {
          this.showInput = true;
          this.showSearching = false;
          this.showSearchResultText = false;
        }
      }
    
    
}
</script>

<style scoped>

h1 {
  color: #2f66A9;
}

.searchWord {
  opacity: 0.5;
}

.search {
  width: 100%;
  position: relative;
  display: flex;
}
.cards {
  position: relative;
  top: 170px;
  left: 50%;
  transform: translateX(-35%);
}
.searchIcon {
  background-color: #ffffff;
  padding-left: 20px;
  padding-right: 20px;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
}

.searchTerm {
  width: 100%;
  padding: 5px;
  height: 35px;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  border: none;
  outline: none;
  color: #6699CC;
  font-weight: bold;
}

.searchTerm:focus{
  color: #3862C6;
  font-weight: bold;
}

::placeholder {
    color: #3862C6;
    font-weight: bold;
}

.wrap{
  width: 80%;
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.search svg {
  height: 15px;
  margin-top: 15px;
}

.headerBox {
  width: 90%;
  height: 190px;
  background-color: #D3D9DF;
  position: absolute;
  top: 15%;
  left: 50%;
  transform: translate(-50%, -50%);
}



@media screen and (max-width: 768px) {
  .cards {
    transform: translateX(-50%);
  }
}



</style>


