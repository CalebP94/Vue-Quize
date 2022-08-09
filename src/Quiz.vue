<template>
  <!-- <pre>{{ JSON.stringify(questions, null, 2) }}</pre> -->

  <section v-if="counter<=4" class="qs">
      <header>
         <h1>COGNITO FORM QUIZ - QUESTIONS</h1>
      </header>
      <form @submit.prevent class="view">

        <ul v-for="(value, index) in questionList" :key='index'>
          <div v-if="index === counter" class="question">
            {{index + 1}}{{".) "}} {{ value.text }}
            <br/>
        
            <div v-for="(answers, index) in value.answers" :key='index'>
              <input type="radio" :id='answers' :value='answers' v-on:input="setObj(value.text,answers)"/>
              <label :for="answers"> {{answers}} </label>
            </div>
          </div>
        </ul>
        <button v-on:click="add">Next</button>
      </form>
  </section>
  <section v-else-if="counter>4" class="qs">
    <header>
      <h1>COGNITO FORM QUIZ - YOUR ANSWERS</h1>
    </header>
    <div v-for="(a, i) in answersArr" :key="'index'" class="view">
      {{i+1}}{{".) "}}{{a.q}} {{a.a}}
    </div>
  </section>
</template>
<script>
export default {
  props: {
    questions: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      counter:1,
      questionList: this.questions,
      answers: {question:'',answer:''},
      answersArr:[],
      answered:false,
    };
  },
  methods:{
    setObj(q, a){
      this.answers.question = q;
      this.answers.answer = a;
      this.answered = true;
    },
    add() {
      console.log(this.counter);
      if(this.counter > this.questions.length -1){
        this.counter= 0
      }
      if(this.answers.question != '' && this.answered){
        let arr = {q: this.answers.question, a: this.answers.answer}
        this.answersArr.push(arr)
        this.counter++;
        this.answered= false;
        console.log(this.answersArr)
      }
    },
    sub(){
      this.counter--;
      console.log(this.counter);
      if(this.counter < 0){
        this.counter= this.questions.length -1
      }
      if(this.answersArr.length!=0){
        this.answersArr.pop()
        console.log(this.answersArr);

      }
    },
  }, 
  mounted(){
    this.add();
    this.sub();
  },
  beforeUpdated(){
    alert("Changed")
  }
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
}
body {
	background-color: #ececec;
	color: rgb(197, 197, 197);
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
	font-size: 2rem;
	margin-bottom: 2rem;
}
button {
	appearance: none;
	outline: none;
	border: none;
	cursor: pointer;
	padding: 0.5rem 1rem;
	background-color: #2cce7d;
	color: #2d213f;
	font-weight: 700;
	text-transform: uppercase;
	font-size: 1.2rem;
	border-radius: 0.5rem;
}
.view{
	background-color: #4b4b4b;
	padding: 1rem;
	width: 100%;
	max-width: 640px;
}
.qs{
  margin-top: 10%;
  
}
.question{
  	color: #8F8F8F;
	  font-size: 1.25rem;
}
</style>
