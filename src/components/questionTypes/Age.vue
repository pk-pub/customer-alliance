<template>
    <div class="row">
        <div class="column">
            <span :class="{
                'age': true,
                'first': true,
                'selected': this.age === '<20'
            }" v-on:click="()=>this.setAge('<20')">&lt;20</span>
            <span :class="{
                'age': true,
                'selected': this.age === '20-29'
            }" v-on:click="()=>this.setAge('20-29')">20-29</span>
            <span :class="{
                'age': true,
                'selected': this.age === '30-39'
            }" v-on:click="()=>this.setAge('30-39')">30-39</span>
            <span :class="{
                'age': true,
                'selected': this.age === '40-49'
            }" v-on:click="()=>this.setAge('40-49')">40-49</span>
            <span :class="{
                'age': true,
                'selected': this.age === '50-59'
            }" v-on:click="()=>this.setAge('50-59')">50-59</span>
            <span :class="{
                'age': true,
                'selected': this.age === '60-69'
            }" v-on:click="()=>this.setAge('60-69')">60-69</span>
            <span :class="{
                'age': true,
                'selected': this.age === '70-79'
            }" v-on:click="()=>this.setAge('70-79')">70-79</span>
            <span :class="{
                'age': true,
                'last': true,
                'selected': this.age === '80+'
            }" v-on:click="()=>this.setAge('80+')">80+</span>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';

    @Component
    export default class Rating extends Vue {
        private age = '';

        setAge(age: string) : void {
            this.age = age;

            this.$emit('changed', age);
        }
    }
</script>

<style scoped lang="scss">
    .age {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        border: 1px solid #CCCCCC;
        width: 3rem;
        height: 3rem;
        padding: 0.3rem 1.2rem 0.3rem 1.2rem;

        &.first {
            border-top-left-radius: 1rem;
            border-bottom-left-radius: 1rem;
        }

        &.last {
            border-top-right-radius: 1rem;
            border-bottom-right-radius: 1rem;
        }

        &:hover {
            cursor: pointer;
            background: #46c4ba;
        }

        &.selected {
            background: #46c4ba;
        }
    }
</style>
