<script setup>
    import  Question from "../components/Question.vue"
    import  QuizHeader from "../components/QuizHeader.vue"
    import {useRoute} from "vue-router"
    import { ref } from 'vue';
    import quizes from "../data/quizes.json"
 

    const route = useRoute()

    const quizId = parseInt(route.params.id);

    const quiz = quizes.find(q => q.id === quizId)
    //Coge el array quizes y mira cada objeto su id y lo compara con quizId
    const currentQuestionIndex = ref(0)

</script>

<template>
    <div>
       
        <QuizHeader />
   
         <Question :question="quiz.questions[currentQuestionIndex]" /> 
       

    </div>
</template>

