<template>
  <div class="container-fluid">
    <div class="homeIntroWrapper mx-auto">
      <div class="hero">
        <h1>Vilka är vi?</h1>
        <div class="description-container">
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Corporis temporibus recusandae ut soluta molestias vel eum vitae, praesentium, optio itaque, deserunt ratione voluptas. Voluptates quaerat, ad placeat laudantium atque ullam ratione animi vitae facere consequuntur porro recusandae explicabo dolorum vel cumque dicta fugiat magni nulla provident minus mollitia pariatur quisquam similique quas? Sit illum, quis aliquid illo quisquam exercitationem officiis est quos commodi magni hic consectetur possimus enim odio alias minima, pariatur ut recusandae ab explicabo? Possimus obcaecati quo officia incidunt provident repellat, beatae quia corporis commodi maiores. Iste, ipsum libero nulla accusantium corrupti expedita qui commodi nobis ducimus similique.</p>
        </div>
      </div>
        

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
    background: linear-gradient(#00000070, transparent), url('../assets/bilder/foretag-grupp-bild.jpeg'), no-repeat;
    background-size: cover;
    padding-block: 5em;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5rem;
  }

  .homeIntroWrapper .hero h1{
    width: 100%;
    font-family: "neo-sans", sans-serif;
    font-style: italic;
    font-size: 10em;
    font-weight: 900;
    text-align: center;
    text-transform: uppercase;
    background: linear-gradient(90deg, #6f58ee, #37229c, #6f58ee) 0 0 / 300% 100%;
    color: transparent;
    -webkit-text-fill-color: transparent;
    -webkit-background-clip: text;
    animation: hero-text-gradient 10s linear infinite;
  }

  @keyframes hero-text-gradient {
   to {
      background-position: 300% 0;
    }
  }

  .homeIntroWrapper .hero .description-container{
    max-width: 800px;
    backdrop-filter: blur(10px);
    background: #00000035;
    border-radius: 5px;
    padding: 1rem;
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