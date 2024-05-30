<template>
  <div class="container-fluid">
    <div class="homeIntroWrapper mx-auto">
      <div class="hero">
      </div>
      <h1>Vilka är vi?</h1>        
        

      <!-- Employees Data -->
      <div class="employees-wrapper">
        <employees-comp :employees="employees"></employees-comp>
      </div>

      <!-- Pagination Controls -->
      <div class="custompagination d-flex align-items-center mb-5">
        <button @click="changePage(pagenum - 1)" :disabled="pagenum === 1">&lt;</button>
          <span v-for="(item, index) in new Array(totalPages)" :key="index">
            <button 
                      @click="changePage(index + 1)"
                      :class="[index + 1 === pagenum ? 'linkactive' : '']">{{ index + 1}}</button>
              </span>
        <button @click="changePage(pagenum + 1)" :disabled="pagenum === totalPages">&gt;</button>
      </div>
      
    </div>
  </div>
</template>

<script>
import EmployeesComp from '../components/EmployeesComp.vue';
export default {
  components: {
    EmployeesComp
  },
  data(){
    return{
        employees: [],
        pagenum: 1,
        totalPages: 0
      }
  },
  created() {
    this.getEmployees();
  },
  methods: {
    async getEmployees(){
      try {
        const res = await fetch('https://reqres.in/api/users?page=' + this.pagenum);
        const data = await res.json();
        this.employees = data.data;
        this.pagenum = data.page;
        this.totalPages = data.total_pages;
        
      } catch (err) {
        return console.error(err);
      }
      
    },
    changePage(num){
      this.pagenum = num;
      this.getEmployees();
    }
  }
}
</script>
<style scoped>
  .homeIntroWrapper{
    width: 100%;
  }

  .homeIntroWrapper .hero{
    background: linear-gradient(#2b2161a5 , transparent), url('../assets/bilder/foretag-grupp-bild.jpeg') center top / cover no-repeat;
    padding-block: 10em;    
  }

  .homeIntroWrapper h1{
    width: 100%;
    font-family: "neo-sans", sans-serif;
    font-style: italic;
    font-size: clamp(5em, 50%, 10em);
    font-weight: 900;
    text-align: center;
    text-transform: uppercase;
    background: linear-gradient(90deg, #6f58ee, #37229c, #6f58ee) 0 0 / 300% 100%;
    color: transparent;
    -webkit-text-fill-color: transparent;
    -webkit-background-clip: text;
    animation: hero-text-gradient 10s linear infinite;
    margin-block: 3rem 1rem;
  }

  @keyframes hero-text-gradient {
   to {
      background-position: 300% 0;
    }
  }

  .homeIntroWrapper .hero .description-container p{    
    font-size: 1.2em;
    color: var(--v-egg-white);    
  }

  .homeIntroWrapper .employees-wrapper{
    max-width: 970px;
    margin: auto;
  }
  
  .homeIntroWrapper .custompagination button{
    border: none;
    background: none;
    font-size: 1.3em;
    transition: all 0.2 ease;
    color: var(--v-main-purple);
    margin: auto;
  }

  .homeIntroWrapper .custompagination button:hover{
    color: var(--v-main-purple);
    transform: scale(1.1);
  }
  
  .homeIntroWrapper .custompagination button:disabled{
    color: rgba(0, 0, 0, 0.072);
  }
  .linkactive{
    text-decoration: underline;
    font-weight: bold;
  }
  
  
@media screen and (max-width: 700px) {
  .homeIntroWrapper p{
    transform: rotateY(0);
  }
    
  .homeIntroWrapper .bildContainer{
    transform: rotateY(180deg);
  }
}

</style>