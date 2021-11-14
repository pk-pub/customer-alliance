<template>
    <div class="row">
        <div class="column col-1">
            <div :class="{
                'rating': true,
                'selected': this.rating === 1
            }" v-on:click="()=>setRating(1)">1</div>
        </div>
        <div class="column col-1">
            <div :class="{
                'rating': true,
                'selected': this.rating === 2
            }" v-on:click="()=>setRating(2)">2</div>
        </div>
        <div class="column col-1">
            <div :class="{
                'rating': true,
                'selected': this.rating === 3
            }" v-on:click="()=>setRating(3)">3</div>
        </div>
        <div class="column col-1">
            <div :class="{
                'rating': true,
                'selected': this.rating === 4
            }" v-on:click="()=>setRating(4)">4</div>
        </div>
        <div class="column col-1">
            <div :class="{
                'rating': true,
                'selected': this.rating === 5
            }" v-on:click="()=>setRating(5)">5</div>
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';

    @Component
    export default class Rating extends Vue {
        private rating = 0;

        setRating(rating: number) : void {
            this.rating = rating;

            this.$emit('changed', rating);
        }
    }
</script>

<style scoped lang="scss">
    .rating {
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: #eeeeee;
        border: 1px solid #bbbbbb;
        width: 3rem;
        height: 3rem;
        border-radius: 5rem;

        &:hover {
            cursor: pointer;
            background: #46c4ba;
        }

        &.selected {
            background: #46c4ba;
        }
    }
</style>
