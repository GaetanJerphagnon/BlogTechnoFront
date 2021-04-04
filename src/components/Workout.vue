<template>
<div class="my-2 col-12 col-md-6">

  <div class="card border-dark m-0 p-0">

    <div class="card-header bg-secondary rounded-0">
       <h3 class="m-0">{{name}}</h3>
       <span :key='t' v-for='t in types' class="badge badge-success ml-2">{{t.description}}</span>
    </div>
    <div class="card-body text-dark bg-white d-flex flex-column flex-md-row ">
        <div class="m-auto">
            <img :src="'http://localhost:8000/pictures/'+techno.image" alt="Image de la techno" class="img-thumbnail border-0" height="200" width="200">
        </div>
        <div class="container-fluid">
            <h5 class="card-title">{{techno.name}}  - {{rating}}</h5>
            <p class="card-text">{{description}}</p>
        </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
    name: 'Workout',
    props: ["name", "rating", "description", "doneAt", "techno", "types"],
}
</script>

<style scoped>
.card{
    border-radius:0;
}

</style>