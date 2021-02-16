<template>
<div class="csv">
    <li v-for="view in views" :key="view">
        {{views.name}}, {{views.status}} !
  </li >
</div>
  
</template>

<script>


export default {
    data(){
        return {
            views:{
               name:'Vue',
               status: 'Works'
            }
        }
    }
}


   
</script>
