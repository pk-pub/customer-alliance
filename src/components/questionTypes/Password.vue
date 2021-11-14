<template>
    <div class="row">
        <div class="column">
            <input type="password" class="input-text" v-on:keyup="setPassword">
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';

    @Component
    export default class Password extends Vue {
        private password = '';

        setPassword(event: any) : void {
            this.password = event.target.value;
            this.$emit('changed', event.target.value);
        }
    }
</script>
