<template>
    <div>   
        <ol class="breadcrumb d-flex justify-content-center bg-dark">
            {{ $route.params.pageNum }}
            <li v-if="previousUrl"><button class="btn btn-sm btn-dark mx-2 rounded-0" @click="reloadWorkouts(previousUrl), changePageNum(false)"><i class="fa fa-arrow-left"></i></button></li>
            <li v-if="!previousUrl" ><button class="btn btn-sm btn-secondary mx-2 rounded-0 disabled"><i class="fa fa-arrow-left"></i></button></li>

            <li><p class="btn btn-sm bg-wheat mx-2 my-0 rounded-0">{{ Math.min(Math.max(pageNum*4, 0), totalItem) }} / {{ totalItem }}</p></li>

            <li v-if="nextUrl"><button class="btn btn-sm btn-dark mx-2 rounded-0" @click="reloadWorkouts(nextUrl), changePageNum(true)"><i class="fa fa-arrow-right"></i></button></li>
            <li v-if="!nextUrl" ><button class="btn btn-sm btn-secondary mx-2 rounded-0 disabled"><i class="fa fa-arrow-right"></i></button></li>
        </ol>
    </div>
    <div class="row p-0 d-flex flex-row">
        <Workout
            :key='w'
            v-for= 'w in workouts'
            :name="w.name"
            :description="w.description"
            :rating="w.rating"
            :techno="w.techno"
            :types="w.types"
        />
    </div>
</template>

<script>
import Workout from '@/components/Workout.vue'
import axios from 'axios'

export default {
    
  name: 'Workouts',
  mounted() { 
      let config ={
                headers: {
                    'Accept': 'Application/ld+json'
                }
            }
            axios.get('http://localhost:8000/api/workouts', config)
            .then(response => (
                this.workouts = response.data['hydra:member'],
                this.currentUrl = response.data['hydra:view']['@id'],
                this.previousUrl = this.getPreviousUrl(this.currentUrl),
                this.nextUrl = response.data['hydra:view']['hydra:next'],
                this.totalItem = response.data['hydra:totalItems']
                ))
            .catch(error => (console.log(error)))
  },
  components: {
      Workout
  },
  data(){
    return {
        totalItem:null,
        pageNum:1,
        workouts: null,
        nextUrl:null,
        previousUrl:null,
        currentUrl:null,
        }
    },
  methods: {
        getPreviousUrl(url){
            let pageNum = url.slice(-1);
            console.log('pageNum '+pageNum);
            url = url.substring(0, url.length - 1);

            if(pageNum == "1"){
                return null;
            } else {
                pageNum--;
                return url+pageNum.toString();
            }
        },
        changePageNum(bool){
            if(bool){this.pageNum++}
            else if(!bool){this.pageNum--};
        },
        async reloadWorkouts(url){
            console.log('api : '+url);
            if(url){
            let config ={
                headers: {
                    'Accept': 'Application/ld+json'
                }
            }
            axios.get('http://localhost:8000'+url, config)
            .then(response => (
                this.workouts = response.data['hydra:member'],
                this.currentUrl = response.data['hydra:view']['@id'],
                this.previousUrl = this.getPreviousUrl(this.currentUrl),
                this.nextUrl = response.data['hydra:view']['hydra:next']
                ))
            .catch(error => (console.log(error)))
            } else {
                console.log('pas d\'url');
            }
        }
    }
}
</script>

<style>

</style>