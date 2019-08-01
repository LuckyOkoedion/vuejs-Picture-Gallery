<template>
<div class="container">
  <router-view></router-view>
</div>
</template>

<script>

export default {
  name: 'app'
}
</script>

<style>

body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  margin-right: auto;
  margin-left: auto;
  padding-right: 15px;
  padding-left: 15px;
  width: 100%;
  max-width: 100%;
}






/* Media Queries */

@media (min-width: 768px) {
  .container{
    width: 750px;
  }
}

@media (min-width: 992px) {
  .container{
    width: 970px;
  }
}

@media (min-width: 1200px) {
  .container{
    width: 1170px;
  }
}


</style>
