<template>
    <div class="row">
        <div class="column">
          <input type="text" class="input-text" v-on:keyup="setEmail">
        </div>
    </div>
</template>

<script lang="ts">
    import { Component, Vue } from 'vue-property-decorator';

    @Component
    export default class Email extends Vue {
        private email = '';

        setEmail(event: any) : void {
            this.email = event.target.value;

            this.$emit('changed', event.target.value);
        }
    }
</script>
