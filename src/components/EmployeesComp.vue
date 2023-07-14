<template>
    <div class="employees my-5" v-if="employees.length > 0">
      <div class="employee" v-for="employee in employees" :key="employee.id">
        <router-link :to="{ name: 'detail', params: { id: employee.id } }">
            <img :src="employee.avatar" width="200" height="200">
            <p class="my-1 text-secondary-title">{{ employee.first_name + ' ' + employee.last_name}}</p>
            <p class="my-4">Kontakt</p>
        </router-link>
      </div>
    </div>
</template>
<script>
export default {
    props: {
        employees: []
    }
    
}
</script>
<style>
    .employees{
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 50px;        
    }

    .employees .employee{
        padding: 1rem;
        text-align: center;
        transition: all 0.2s ease;

    }
    
    .employees .employee:hover{
        box-shadow: 
            2px 2px 10px 1px rgba(0, 0, 255, .2), 
            inset 2px 2px 10px 1px rgba(0, 0, 0, 0.061);
        transform: scale(1.1);
    }

    .employees .employee p:last-child{
        font-weight: 500;
        background: -webkit-linear-gradient(#9280e8, #4524ed);
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }
    
    .employees .employee img{
        border-radius: 50%;
        object-fit: cover;
    }

    @media screen and (max-width: 1000px) {
        .employees{
            grid-template-columns: 1fr 1fr;
        }
        
    }

    @media screen and (max-width: 700px) {
        .employees{
            grid-template-columns: 1fr;
        }
        
    }
</style>