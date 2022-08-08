<template>
  <!-- <pre>{{ JSON.stringify(questions, null, 2) }}</pre> -->
  <div>
      <form>
            <li v-for="(data, index) in questionArr" :key='index'>
              {{ questionArr }}
            </li>
      </form>
      <button v-on:click="add">Next</button>
      <button v-on:click="sub">Previous</button>
  </div>
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
      counter:0,
      questionList: this.questions,
      questionArr:[],
      answers:[],
    };
  },
  //access props
  //create functions that interact with globals (this) & objects returned in data
  methods:{
    add() {
      this.counter++;
      console.log(this.counter);
      if(this.counter > 4){
        this.counter= 0
      }
    },
    sub(){
      this.counter--;
      console.log(this.counter);
      if(this.counter < 0){
        this.counter=4
      }
    },
    questionsBlah(){
        //console.log(this.questionList.answers)
        let quiz = this.questionList;
        quiz.map((i) => questionArr.push(i.text))
        const answers = quiz.map((i)=> console.log(i))
    }
  }, 
  mounted(){
    this.add();
    this.sub();
    //this.questionsBlah()
  },
  beforeUpdate(){
      alert("beforeUpdated");
  },
};
</script>
