<template>
    <div>
        <div class="row">
            <div class="column">
                <div class="index">{{index+1}}.</div>
                <span class="question">{{question.label}}</span>
                <span v-if="question.validation.required===true" class="required">(required)</span>
            </div>
        </div>
        <Rating v-if="question.type === 'rating'" v-on:changed="updateAnswer"/>
        <Age v-if="question.type === 'age'" v-on:changed="updateAnswer"/>
        <Email v-if="question.type === 'email'"  v-on:changed="updateAnswer"/>
        <Password v-if="question.type === 'password'"  v-on:changed="updateAnswer"/>
    </div>
</template>

<script lang="ts">
    import { Component, Prop, Vue } from 'vue-property-decorator';
    import Rating from "@/components/questionTypes/Rating.vue";
    import Age from "@/components/questionTypes/Age.vue";
    import Email from "@/components/questionTypes/Email.vue";
    import Password from "@/components/questionTypes/Password.vue";

    @Component({
        components: {Password, Email, Age, Rating}
    })
    export default class Question extends Vue {
        @Prop() private question!: string;
        @Prop() private index!: number;
        updateAnswer(answer : any) : void {
            this.$emit('changed', answer, this.index);
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    h3 {
        color: #3b62b2;
    }
    .index {
        font-size: 16pt;
        font-weight: bold;
        color: #3b62b2;
    }
    .question {
        color: #265364;
        font-size: 16pt;
    }
    .required {
        color: #CCCCCC;
        margin-left: 0.3rem;
    }
</style>
