<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadExperiences">Load Submitted Experiences</base-button>
      </div>
      <ul>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from "./SurveyResult.vue";
import axios from "axios";
export default {
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
    };
  },
  methods: {
    loadExperiences() {
      axios
        .get("https://survey-2070f-default-rtdb.firebaseio.com/surveys.json")
        .then((res) => {
         const data=res.data;
         const results=[];
         for(const id in res.data){
           results.push({id:id , name:data[id].name, rating:data[id].rating})
         }
          // console.log(res.data);
          this.results=results;
          
        })
        

      // fetch("https://survey-2070f-default-rtdb.firebaseio.com/surveys.json")
      // .then(response=>{
      //   if(response.ok){
      //     return response.json();
      //   }
      // })
      // .then(data=>{
      //   console.log(data);
      // })
       
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
