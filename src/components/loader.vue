<template>

<div class="pictureframes">

    
    <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>

    <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>
    
    <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>

    <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>

     <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>

    <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>

    <div class="column">
      <div class="img"></div>
      <span class="title"></span>
      <span class="author"></span>
    </div>


</div>



    
</template>

<script>

export default {
    name: 'Loader'
    
}


</script>

<style scoped>
/* Style for the cards */

.title {
  position: absolute;
  display: block;
  left: 5%;
  top: 75%;
  height: 18px;
  /* width: 100px; */
  background-color: #E5E1D6;
  animation: grow 0.5s infinite;

}

.author {
  position: absolute;
  display: block;
  left: 5%;
  top: 90%;
  height: 18px;
  /* width: 70px; */
  background-color: #E5E1D6;
  animation-delay: 0.3s;
  animation: growshort 0.5s infinite;

}

@keyframes grow {
  from {width: 10px;}
  to {width: 100px}
  
}

@keyframes growshort {
  from {width: 10px;}
  to {width: 70px}
  
}

.img {
  width: 100%;
  height: 100%;
  background-color: #EBEBEB;
  
}

.column:nth-child(1) {
  position: absolute;
    height: 180px;
}

.column:nth-child(2) {
  position: absolute;
   left: 23%;
    height: 250px;
}

.column:nth-child(3) {
  position: absolute;
  left: 47%;
    height: 210px; 
}

.column:nth-child(4) {
    position: absolute;
    top: 240px;
    height: 240px;
}

.column:nth-child(5) {
    position: absolute;
    left: 23%;
    top: 310px;
    height: 210px;
}

.column:nth-child(6) {
    height: 250px; 
    position: absolute;
    left: 47%;
    top: 270px;
}

.column:nth-child(7) {
  position: absolute;
  top: 580px;
  left: 23%;
  height: 210px;
    /* height: 200px; */
}



/* Float four columns side by side */


.column {
  float: left;
  width: 20%;
  padding: 0px;
  margin-right: 40px;
  margin-bottom: 30px;
  display: absolute;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0); /* this adds the "card" effect */
}



/* Responsive columns - one column layout (vertical) on small screens */
@media screen and (max-width: 600px) {
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
    margin-right: 20px;
  }
  .column:nth-child(1) {
    position: absolute;
    top: 0px;

  }
   .column:nth-child(2) {
     position: absolute;
     left: 0%;
     top: 240px;
  }
   .column:nth-child(3) {
     position: absolute;
     left: 0%;
     top: 550px;
    
  }
   .column:nth-child(4) {
     position: absolute;
     top: 820px;
    
  }
   .column:nth-child(5) {
     top: 1120px;
     left: 0%;
    
  }
   .column:nth-child(6) {
    position: absolute;
    top: 1390px;
    left: 0px;
  }
   .column:nth-child(7) {
     position: absolute;
     top: 1700px;
     left: 0%;
    
  }
}

</style>


