<template>
  <div class="container">
    <a class="link-custom my-5" @click="$router.go(-1)">
      &lt; Tillbaka
    </a>

    <div class="employeeWrapper">
      <div class="employeeItems">
        <img :src="employee.avatar" width="200" height="200">
        <p class="text-secondary-title">{{ employee.first_name }} {{ employee.last_name }}</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus est enim consequatur autem harum omnis mollitia non numquam id quod minus quas dolores, quibusdam tempora nostrum. Maxime, neque perspiciatis aspernatur delectus ipsam maiores velit iste sed dignissimos commodi ad eos tempore! Quis quibusdam natus quasi voluptatibus necessitatibus sunt recusandae nemo.</p>
        <a class="link-custom" :href="'mailto:' + employee.email">
          {{ employee.email }}
        </a>
      </div>
    </div>
  </div>
</template>
<script>
    export default{
    props: ['id'],
    data(){
      return{
        employee: {
          id: '',
          email: '',
          first_name: '',
          last_name: '',
          avatar: '',
        }
      }
    },
    created() {
      this.getEmployee();
    },
    methods: {
      async getEmployee(){
        try {
          const res = await fetch(`https://reqres.in/api/users/${this.id}`);
          const data = await res.json();
          return this.employee = data.data;
        } catch (err) {
          return console.error(err);
        }
      }
    }
  }
</script>
<style scoped> 
  .employeeWrapper{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .employeeWrapper .employeeItems{
    max-width: 500px;
    background-color: var(--v-pure-white);
    padding: 1rem;
    border-radius: 5px;
    display: flex;
    flex-direction: column;
    box-shadow: 
        0px 10px 100px 1px rgba(0, 0, 255, .2);
    animation: boxShadowEffect 0.7s cubic-bezier(0.250, 0.460, 0.450, 0.940) both;
  }
  .employeeWrapper .employeeItems img{
    align-self: center;
    border-radius: 50%;
    margin-top: -110px;
    border: 10px solid var(--v-pure-white);
    object-fit: cover;
  }  
  .employeeItems > :nth-child(2),
  .employeeItems > :nth-child(4){
    text-align: center;
  }

  @keyframes boxShadowEffect {
  0% {
    box-shadow: none;
  }
  100% {
    transform: scale(1.1);
    background: var(--v-pure-white);
    box-shadow: 
      0px 10px 100px 1px rgba(0, 0, 255, .2);
  }
}
</style>
