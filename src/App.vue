<script lang="ts" setup>
import DialogWindow from "./components/DialogWindow.vue";
import Header from "./components/Header.vue";
import Switch from "./components/Switch.vue";

import {ref} from 'vue'

const alwaysTrue = ref(true);
const alwaysFalse = ref(false);
</script>
<template>
    <section class="section section--centered">
        <Switch/>
    </section>
    <Header/>
    <section class="section">
        <article>
            <DialogWindow :is-modal="alwaysTrue"/>
            <DialogWindow :is-modal="alwaysFalse"/>
        </article>
    </section>
</template>
