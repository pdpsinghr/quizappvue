<template>
  <div id="app" v-cloak>
    <div class="row">
    <div class="large-12 columns">
      <h1>{{ quiz.title }}</h1>

      <div class="callout">

        <div v-for="(question, index) in quiz.questions">
          <!-- Hide all questions, show only the one with index === to current question index -->
          <div v-show="index === questionIndex">
            <h3>{{ question.text }}</h3>
            <ol>
              <!-- for each response of the current question -->
              <li v-for="response in question.responses">
                <label>
                  <input type="radio"
                           v-bind:value="response.value"
                           v-bind:name="index"
                           v-model="userResponses[index]"> {{response.text}}
                         </label>
              </li>

            </ol>
            <!-- The two navigation buttons -->
            <!-- Note: prev is hidden on first question -->
            <button class="buttonClass" v-if="questionIndex > 0" v-on:click="prev">
              prev
            </button>
            <button class="buttonClass" v-on:click="next">
              next
            </button>
          </div>
        </div>

        <!-- Last page, quiz is finished, display result -->
        <div v-show="questionIndex === quiz.questions.length">
          <h3>Your Results</h3>
          <p>
            You are: {{ score() }}
          </p>
        </div>

      </div>

    </div>
  </div>

</div>
</template>

<script>
/* eslint-disable */
import jsonData from '../../static/quizQuestion.json'
export default {
  name: 'HelloWorld',
  data () {
    return {
      quiz: jsonData,
      questionIndex: 0,
      userResponses: []
    }
  },
  mounted () {
    // this.quiz =
  },
  methods: {
    next: function () {
      this.questionIndex++
      console.log(this.userResponses)
    },
    prev: function () {
      this.questionIndex--
    },
    score: function () {
      console.log(this.userResponses[0])
      var modeMap = {}
      var maxEl = this.userResponses[0],
      maxCount = 1
      for (var i = 0; i < this.userResponses.length; i++) {
        var el = this.userResponses[i]
        if (modeMap[el] == null) modeMap[el] = 1
        else { modeMap[el]++ }
        if (modeMap[el] > maxCount) {
          maxEl = el
          maxCount = modeMap[el]
        }
      }
      return maxEl
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.buttonClass {
  height: 27px;
  width: 53px;
  border: none;
  background: cadetblue;
  border-radius: 10px;
  margin: auto;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
