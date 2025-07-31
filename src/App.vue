<script lang="ts" setup>
import DialogWindow from "./components/DialogWindow.vue";
import Header from "./components/Header.vue";
import Switch from "./components/Switch.vue";
import Tooltip from "./components/Tooltip.vue";
import 'tippy.js/dist/tippy.css';

import {ref} from 'vue'

const alwaysTrue = ref(true);
const alwaysFalse = ref(false);
</script>
<template>
    <Header />
    <article class="page">
        <main class="page__main">
            <section class="section section--switch">
                <Switch />
            </section>
            <section class="section">
                <article class="article">
                    <h2 class="article__title">Modals</h2>
                    <div class="article__main">
                        <DialogWindow :is-modal="alwaysTrue" />
                        <DialogWindow :is-modal="alwaysFalse" />
                    </div>
                </article>
                <article class="article">
                    <h2 class="article__title">Tooltips</h2>
                    <div class="article__main">
                        <Tooltip content="This is a tooltip. It MUST have a parent." />
                        <Tooltip content="This one is visible on CLICK"
                                 type="click"
                        />
                        <Tooltip content="This one is visible on FOCUS"
                                 type="focus"
                        />
                    </div>
                </article>
            </section>
        </main>
        <aside class="page__aside"></aside>
    </article>
</template>
<style lang="scss" scoped>
.page {
    display: grid;
    grid-template-columns: 7fr 3fr;
    height: 100%;
    width: 100%;
}

.page__main {
    padding: 8px 32px;
}

.page__aside {
    padding: 8px 0;
    background-color: wheat;
}

.section {
    display: flex;
    gap: 16px;
    margin: 64px auto;
    padding: 16px;
}

.section--centered {
    margin: auto;
    align-items: center;
    justify-content: center;
    text-align: center;
}

.article {
    display: flex;
    flex-direction: column;
    gap: 16px;
    padding: 16px;
    border: 1px dashed lightgray;
    border-radius: 10px;
}

.article__title {
    font-size: 40px;
}

.article__main {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
}
</style>
