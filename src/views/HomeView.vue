<template>
  <div class="container-fluid">
    <div class="homeIntroWrapper mx-auto">
        <h1>Vilka är vi?</h1>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Corporis temporibus recusandae ut soluta molestias vel eum vitae, praesentium, optio itaque, deserunt ratione voluptas. Voluptates quaerat, ad placeat laudantium atque ullam ratione animi vitae facere consequuntur porro recusandae explicabo dolorum vel cumque dicta fugiat magni nulla provident minus mollitia pariatur quisquam similique quas? Sit illum, quis aliquid illo quisquam exercitationem officiis est quos commodi magni hic consectetur possimus enim odio alias minima, pariatur ut recusandae ab explicabo? Possimus obcaecati quo officia incidunt provident repellat, beatae quia corporis commodi maiores. Iste, ipsum libero nulla accusantium corrupti expedita qui commodi nobis ducimus similique.</p>

        <div class="bildContainer"></div>

      <!-- Employees Data -->
      <employees-comp :employees="employees"></employees-comp>

      <!-- Pagination Controls -->
      <div class="custompagination mb-5">
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
    max-width: 800px;
    margin: 0 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    perspective: 1000px;
  }
  .homeIntroWrapper h1{
    font-family: 'designer';
    font-size: 5em;
    font-weight: bold;
    background: -webkit-linear-gradient(#9280e8, var(--v-main-purple));
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    margin: 3.5rem 0 2.5rem;
  }

  .homeIntroWrapper p{
    max-width: 90%;
    background-color: var(--v-pure-white);
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 
      2px 2px 10px 1px rgba(0, 0, 255, .2), 
      inset 2px 2px 10px 1px rgba(0, 0, 0, 0.061);
    transition: all 0.5s ease;
    transform: rotateY(10deg);
  }

  .homeIntroWrapper p:hover{
    box-shadow: 
      7px 7px 10px 1px rgba(0, 0, 255, .2);
    transform: rotateY(0) scale(1.1);
  }
  
  .homeIntroWrapper .bildContainer{
    width: 30em;
    height: 20em;
    background-image: linear-gradient(rgba(18, 18, 18, 0.647), rgba(67, 64, 64, 0.214)), url('../assets/bilder/foretag-grupp-bild.jpeg');
    background-size: cover;
    background-position: center;
    color: #fff;
    border-radius: 4px;
    box-shadow: 
      2px 2px 10px 1px rgba(0, 0, 255, .2), 
      inset 2px 2px 10px 1px rgba(0, 0, 0, 0.061);
    transition: all 0.5s ease;
    transform: rotateY(170deg);
    margin: 2rem 0 3rem 2rem;
    z-index: -1;
  }
  .homeIntroWrapper .bildContainer:hover{
    box-shadow: 
      7px 7px 10px 1px rgba(0, 0, 255, .2);
    transform: rotateY(180deg) scale(1.1);
  }
  

  .homeIntroWrapper .custompagination button{
    border: none;
    background: none;
    font-size: 1.3em;
    transition: all 0.2 ease;
    color: var(--v-main-purple);
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