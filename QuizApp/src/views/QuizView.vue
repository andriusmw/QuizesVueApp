<script setup>
    import  Question from "../components/Question.vue"
    import  QuizHeader from "../components/QuizHeader.vue"
    import {useRoute} from "vue-router"
    import { ref, watch } from 'vue';
    import quizes from "../data/quizes.json"
 

    const route = useRoute()

    const quizId = parseInt(route.params.id);

    const quiz = quizes.find(q => q.id === quizId)
    //Coge el array quizes y mira cada objeto su id y lo compara con quizId
    const currentQuestionIndex = ref(0)

    const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)

    watch(() => currentQuestionIndex.value, () => {
        //this watch each time the current question index changes
        questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
    })
</script>

<template>
    <div>
       
        <QuizHeader 
        :questionStatus="questionStatus"
        />
   
         <Question :question="quiz.questions[currentQuestionIndex]" /> 
       
    <button @click="currentQuestionIndex++">Next Question</button>
    </div>
</template>

