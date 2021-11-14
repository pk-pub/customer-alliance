<template>
    <div class="container">

        <div class="row">
            <div class="column">
                <h2>Customer Alliance Form</h2>
            </div>
        </div>

        <form v-on:submit="submit">
            <Question v-for="(question, index) of questions"
                      v-on:changed="onAnswer"
                      :key="question.id"
                      :question="question"
                      :index="index"
            />
            <div class="row">
                <div class="column submit">
                    <button type="submit">Submit</button>
                </div>
            </div>
            <div class="row" v-if="formSubmitted === true">
                <div class="column">
                    <span v-if="formValid === true" class="valid">Success</span>
                    <span v-else class="invalid">Not valid</span>
                </div>
            </div>
        </form>

        <div class="results" v-if="answeredQuestions().length > 0" >
            <div class="row" v-for="(question) of answeredQuestions()" :key="question.id">
                <div class="column">
                    <div class="question">{{question.label}}</div>
                    <div class="answer">{{question.answer}}</div>
                </div>
            </div>
            <hr />
            <div class="row">
                <div class="column date">
                   DATE OF EXPERIENCE: {{currentDate()}}
                </div>
            </div>
        </div>

    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import importedQuestions from '@/assets/json/questions.json';
    import Question from "@/components/Question.vue";
    @Component({
        components: {Question}
    })
    export default class Questionaire extends Vue {
        private questions: any = importedQuestions.questions;
        private formValid = false;
        private formSubmitted = false;

        // a question was answered
        private onAnswer(value: any, index: number): void {
            // update the answered question
            this.questions[index].answer = value;

            // required to update results box
            // probably there is a better way to do this in vue
            // but i didnt find it in the available time
            this.$forceUpdate();
        }

        // only return questions that have been answered
        answeredQuestions() : any {
            return this.questions.filter((question : any) => {
                return question.answer !== undefined;
            });
        }

        // get the current date
        currentDate() : any {
            let today : any = new Date();
            let dd : any = today.getDate();

            let mm : any = today.getMonth()+1;
            let yyyy = today.getFullYear();
            if(dd<10)
            {
                dd='0'+dd;
            }

            if(mm<10)
            {
                mm='0'+mm;
            }
            today = yyyy+'/'+dd+'/'+mm;

            return today;
        }

        // the form was submitted
        submit(event: any) {
            event.preventDefault();

            this.formSubmitted = true;
            this.formValid = true;
            // check validity of entries
            for(const question of this.questions) {
                  if(question.type === 'email' && question.validation.required === true) {
                      const regexp =  /(.+)@(.+){2,}\.(.+){2,}/;
                      const check = regexp.test(question.answer);
                      this.formValid = regexp.test(question.answer);
                      if(!check) {
                          break;
                      }

                  } else if(question.type === 'password' && question.validation.required === true) {
                      const regexp = /^(?=.*\d)(?=.*[a-z]).{2,20}$/;
                      const check = regexp.test(question.answer);
                      this.formValid = check;
                      if(!check) {
                          break;
                      }
                  } else if(question.validation.required === true) {
                      const check = question.answer !== undefined;
                      this.formValid = check;

                      if(!check) {
                          break;
                      }
                  }
            }
        }
    }
</script>

<style scoped lang="scss">
    h2 {
        color: #3b62b2;
    }
    .question {
        color: #265364;
        font-weight: bold;
    }
    .answer {
        color: #265364;
    }
    .results {
        padding: 1.5rem;
        position: fixed;
        top: 10%;
        right: 17%;
        width: 20rem;
        border-radius: 1rem;
        background: #f4f4f4;
        box-shadow: 3px -1px 38px 0px rgba(187,187,187,1);
        @media only screen and (max-width: 600px) {
            display: none;
        }

        hr {
            border:1px solid red;
        }

        .date {
            color: #3b62b2;
            text-align: center;
            font-weight: bold;
        }
    }

    .submit {
        text-align: right;

        button {
            cursor: pointer;
            background: #46c4ba;
            padding: 1rem;
            border-radius: 0.5rem;
            color: #FFFFFF;
        }
    }
    .valid {
        color: green;
    }
    .invalid {
        color: red;
    }
</style>
