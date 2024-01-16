<script setup>
  import q from "../data/quizes.json"
  import {ref, watch} from "vue"

    import Card from "../components/Card.vue"

  const quizes = ref(q)
  const search = ref("")
  

//Función de filtro
watch(search, () => {
  quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))
})
/* el Watch vigila si cambia search, cuando cambia hacemos la lógica.
Esta función filtra el estado quizes que es un array, de objetos y los
mira uno por uno que el .name de esos objetos en minusculas  INCLUYA
el valor de search en minuscula; search es ele stado del input/buscador

*/

const beforeEnter = () => {
  console.log("before enter")
}


const enter = () => {
   console.log("entering")
}

const afterEnter = () => {
 console.log("after enter")
}
</script>


<template>
  <div>
   
      <header>
        <h1>Quizes</h1>
        <input v-model.trim="search" type="text" placeholder="Search...">
      </header>
      <div class="options-container">
        <TransitionGroup 
          name="card" 
          appear
          @before-enter="beforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          >
             <Card 
             v-for="quiz in quizes"
            :key="quiz.id" 
            :quiz="quiz"
       
            />
        </TransitionGroup>
 
      </div>
  </div>
</template>



<style scoped>


  header {
    margin-bottom: 10px;
    margin-top: 30px;
    margin-left: 30px;
    display: flex;
    align-items: center;
  }

  header h1 {
    font-weight: bold;
    margin-right: 30px;
  }

  header input {
    border: none;
    background-color: rgba(128,128,128,0.1);
    padding: 10px;
    border-radius: 5px;
  }

  .options-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
    margin-left: 30px;
  }

  .card-enter-from {
    transform: translateY(-50px);
    opacity: 0;
  }

  .card-enter-to {
     transform: translateY(0px);
    opacity: 1;
  }

  .card-enter-active {
    transition: all 0.4s ease;
  }
</style>