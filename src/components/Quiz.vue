<template>
  <div class="container">
    <div class="row">
      <div class="col-md-7 quiz">
        <div class="card quiz-app">
          <div class="quiz-header">
            <h1 class="card-title">quiz-app</h1>
          </div>
          <div
            class="quiz-main"
            v-for="(element, index) in randomQuestions.slice(a, b)"
            :key="index"
            v-show="quizBox"
          >
            <div class="quiz-question">
              <h3>Question {{ b }} / {{ randomQuestions.length }}</h3>
              <p>{{ element.question }}</p>
            </div>
            <div class="quiz-suggestions">
              <ul>
                <li
                  v-for="(item, index) in element.suggestions"
                  :key="index"
                  :class="select ? check(item) : ''"
                  @click="selectAnswer(item)"
                >
                  {{ item.suggestion }}
                </li>
              </ul>
            </div>
          </div>
        
          <div class="score" v-show="scoreShow">
            <h3>Your Score Is :</h3>
            <h1>{{ score }}</h1>
            <p>{{scoreMessage}}</p>
            <button @click="restart">Restart</button>
          </div>
          <div class="quiz-footer">
            <button @click="skip()">skip</button>
            <button @click="nextQuestion()">next</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      questions: [
        {
          question: "Which type of JavaScript language is",
          suggestions: [
            { suggestion: "Object-Oriented" },
            { suggestion: "Object-Based", correct: true },
            { suggestion: "Assembly-language" },
            { suggestion: "High-level" },
          ],
        },
        {
          question:
            "Which one of the following also known as Conditional Expression",
          suggestions: [
            { suggestion: "Alternative to if-else" },
            { suggestion: "Switch statement" },
            { suggestion: "If-then-else statement" },
            { suggestion: "immediate if", correct: true },
          ],
        },
        {
          question: "The 'function' and 'var' are known as:",
          suggestions: [
            { suggestion: "Keywords" },
            { suggestion: "Data types" },
            { suggestion: "Declaration statements", correct: true },
            { suggestion: "Prototypes" },
          ],
        },
        {
          question: "Which of the following type of a variable is volatile?",
          suggestions: [
            { suggestion: "Mutable variable", correct: true },
            { suggestion: "Dynamic variable" },
            { suggestion: "Volatile variable" },
            { suggestion: "Immutable variable" },
          ],
        },
        {
          question:
            "Which of the following number object function returns the value of the number?",
          suggestions: [
            { suggestion: "toString()" },
            { suggestion: "valueOf()", correct: true },
            { suggestion: "toLocaleString()" },
            { suggestion: "toPrecision()" },
          ],
        },
        {
          question: " In JavaScript the x===y statement implies that:",
          suggestions: [
            {
              suggestion:
                "Both x and y are equal in value, type and reference address.",
            },
            { suggestion: "Both are x and y are equal in value only." },
            {
              suggestion: "Both are equal in the value and data type.",
              correct: true,
            },
            { suggestion: "Both are not same at all." },
          ],
        },
        {
          question:
            " In JavaScript, what will be used for calling the function definition expression:",
          suggestions: [
            { suggestion: "Function prototype" },
            { suggestion: "Function literal", correct: true },
            { suggestion: "Function calling" },
            { suggestion: "Function declaration" },
          ],
        },
        {
          question: "  Which one of the following is an ternary operator:",
          suggestions: [
            { suggestion: "?", correct: true },
            { suggestion: ":" },
            { suggestion: "+" },
            { suggestion: "-" },
          ],
        },
        {
          question:
            "Which one of the following operator returns false if both values are equal?",
          suggestions: [
            { suggestion: "!" },
            { suggestion: "!==" },
            { suggestion: "!=", correct: true },
            { suggestion: "All of the above" },
          ],
        },
        {
          question:
            "Which one of the following is not considered as 'statement' in the JavaScript?",
          suggestions: [
            { suggestion: "use strict", correct: true },
            { suggestion: "debugger" },
            { suggestion: "if" },
            { suggestion: "with" },
          ],
        },
        {
          question:
            " A set of unordered properties that, has a name and value is called",
          suggestions: [
            { suggestion: "String" },
            { suggestion: "Array" },
            { suggestion: "Serialized Object" },
            { suggestion: "Object", correct: true },
          ],
        },
        {
          question: "  The linkage of a set of prototype objects is known as",
          suggestions: [
            { suggestion: "prototype" },
            { suggestion: "prototype stack" },
            { suggestion: "prototype class" },
            { suggestion: "prototype chain", correct: true },
          ],
        },
        {
          question: " If a function which does not return a value is known as",
          suggestions: [
            { suggestion: "Static function" },
            { suggestion: "Procedures", correct: true },
            { suggestion: "Method" },
            { suggestion: "Dynamic function" },
          ],
        },
        {
          question:
            " What happens if the return statement has no related expression?",
          suggestions: [
            { suggestion: "It will return a undefined value", correct: true },
            { suggestion: "It will throw a exception" },
            { suggestion: "It will return the 0 as the value" },
            { suggestion: "It will throw a error" },
          ],
        },
        {
          question: "Which one of the following is not a example of closures?",
          suggestions: [
            { suggestion: "Graphics", correct: true },
            { suggestion: "Variables" },
            { suggestion: "Functions" },
            { suggestion: "Objects" },
          ],
        },
        {
          question: "In JavaScript, what kind of scoping is used?",
          suggestions: [
            { suggestion: "Literal scoping" },
            { suggestion: "Sequential scoping" },
            { suggestion: "Segmental scoping" },
            { suggestion: "Lexical scoping", correct: true },
          ],
        },
        {
          question: "Which of the following is not JavaScript Data Types?",
          suggestions: [
            { suggestion: " Undefined" },
            { suggestion: " Number" },
            { suggestion: " Boolean" },
            { suggestion: "Float", correct: true },
          ],
        },
        {
          question: " Inside which HTML element do we put the JavaScript?",
          suggestions: [
            { suggestion: "<script>", correct: true },
            { suggestion: " <head>" },
            { suggestion: "<meta>" },
            { suggestion: "<style>" },
          ],
        },
        {
          question: "  What is the original name of JavaScript?",
          suggestions: [
            { suggestion: " LiveScript" },
            { suggestion: "  EScript" },
            { suggestion: " Mocha", correct: true },
            { suggestion: "JavaScript" },
          ],
        },
      ],
      randomQuestions: [],
      a: 0,
      b: 1,
      select: false,
      score: 0,
      quizBox: true,
      scoreShow: false,
      scoreMessage: "",
    };
  },
  mounted() {
    while (this.randomQuestions.length < 10) {
      var item = this.questions[
        Math.floor(Math.random() * this.questions.length)
      ];
      if (this.randomQuestions.indexOf(item) === -1) {
        this.randomQuestions.push(item);
      }
    }
  },
  methods: {
    check(answer) {
      if (answer.correct) {
        return "correct";
      } else {
        return "incorrect";
      }
    },
    selectAnswer(anscorect) {
      this.select = true;
      if (anscorect.correct) {
        this.score++;
      }
    },
    nextQuestion() {
      if (this.b == 10) {
        this.quizBox = false;
        this.scoreShow = true;
        if (this.score == 10 && this.score > 8) {
          this.scoreMessage = "Well Done , You Are Genius .";
        } else if (this.score > 4 && this.score < 8) {
          this.scoreMessage = "You can succeed, work hard and keep going .";
        } else {
          this.scoreMessage =
            "Your current level does not qualify you to work, you must strive to reach.";
        }
      } else {
        this.a++;
        this.b++;
        this.select = false;
      }
    },
    skip() {
      this.quizBox = false;
      this.scoreShow = true;
      if (this.score == 10 && this.score > 8) {
        this.scoreMessage = "Well Done , You Are Genius .";
      } else if (this.score > 4 && this.score < 8) {
        this.scoreMessage = "You can succeed, work hard and keep going .";
      } else {
        this.scoreMessage =
          "Your current level does not qualify you to work, you must strive to reach.";
      }
    },
    restart() {
      location.reload();
    },
  },
};
</script>

<style>
.quiz {
  margin: auto;
}
.quiz-header {
  padding: 40px 0px;
  background-color: #ddd;
  color: #555;
  text-transform: uppercase;
}
.quiz-footer {
  background-color: #ddd;
  padding: 20px 0px;
}
.quiz-header h1 {
  font-size: 30px;
  margin: 0;
  letter-spacing: 1px;
  font-weight: 700;
}
ul {
  margin: 0;
  list-style: none;
  width: 90%;
}
li {
  padding: 10px 0px;
  line-height: 1.5;
  border: 1px solid #aaa;
  margin-bottom: 20px;
  border-radius: 30px;
}
li:hover {
  background-color: #ddd;
  cursor: pointer;
}
li.correct {
  background-color: rgb(74, 219, 74);
  border: 1px solid rgb(74, 219, 74);
  color: #ffffff;
}
li.incorrect {
  background-color: rgb(240, 117, 100);
  border: 1px solid rgb(240, 117, 100);
  color: #ffffff;
}
.quiz-question {
  margin: 30px 0px;
}
.quiz-question p {
  margin: 10px 0px;
}
.quiz-footer button {
  background: #555;
  color: #ddd;
  padding: 3px 25px;
  font-size: 18px;
  border-radius: 30px;
  border: 1px solid #aaa;
  outline: none;
  margin: 1% 10% auto;
  transition: .5s;
}
.quiz-footer button:hover{
    color: #555;
    background-color: #ddd;
}
.score {
  padding: 90px 0px;
}
.score button {
  background: rgb(0, 81, 255);
  border: 1px solid #aaa;
  padding: 5px 30px;
  outline: none;
  color: #ffffff;
  letter-spacing: 1px;
  border-radius: 30px;
  transition: .5s;
}
.score button:hover{
    background: none;
    color: #555;
}
.score p{
    color: #555;
    text-transform: capitalize;
    font-weight: 600;
    margin: 30px 0px;
   font-size: 13px;
}
</style>