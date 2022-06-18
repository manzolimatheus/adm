<template>
  <MainHeader/>
  <main>
    <router-view/>
  </main>
</template>

<script>
import MainHeader from './components/MainHeader.vue';
export default {
  components:{
    MainHeader
}
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

*{
  margin: 0;
  padding: 0;
  font-family: 'Montserrat', sans-serif;
}

h1, h2, h3, h4, h5, h6{
  font-family: 'Nunito', sans-serif;
}

a{
  text-decoration: none;
}

img{
  max-width: 100%;
}

main{
  padding: 4%;
}

#form {
  margin-top: 4%;
}
.w-50 {
  width: 50%;
}

.row {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
}

@media (max-width: 768px) {
  .row {
    grid-template-columns: 100%;
  }
}

.form-group {
  margin-bottom: 2%;
}

input {
  border-radius: 5px;
  border: 1px solid lightgrey;
  font-size: 16pt;
  padding: 1%;
  margin: 1%;
}

hr {
  border: 1px solid lightgrey;
  margin-top: 2%;
  margin-bottom: 2%;
}

</style>
