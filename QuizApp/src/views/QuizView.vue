<script setup>
    import  Question from "../components/Question.vue"
    import  QuizHeader from "../components/QuizHeader.vue"
    import {useRoute} from "vue-router"
    import { ref, watch, computed } from 'vue';
    import quizes from "../data/quizes.json"
 

    const route = useRoute()

    const quizId = parseInt(route.params.id);

    const quiz = quizes.find(q => q.id === quizId)
    //Coge el array quizes y mira cada objeto su id y lo compara con quizId

    //1-this defines the state
    const currentQuestionIndex = ref(0)
    //-------------------------------------------------------------------------------------------
    /*
    const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)
    //2-this watchs when the states changes and do the action we say
    watch(() => currentQuestionIndex.value, () => {
        //this watch each time the current question index changes
        questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
        // this translates as for example:       "1 "        "/ "     "3"
    }) */
    // ------------------------------------------------------------------------------
    // 3- Computed actually does the same as line 17 to 26.
const questionStatus = computed(() => {
    return `${currentQuestionIndex.value}/${quiz.questions.length}`
})

const barPercentage = computed(() => {
    return `${currentQuestionIndex.value/quiz.questions.length * 100}%`
    // This is the math operation for obtaining the % of completion but using variables
} )

</script>

<template>
    <div>
       {{barPercentage}}
        <QuizHeader 
        :questionStatus="questionStatus"
        :barPercentage="barPercentage"
        />
   
         <Question :question="quiz.questions[currentQuestionIndex]" /> 
       
    <button @click="currentQuestionIndex++">Next Question</button>
    </div>
</template>

