<script lang="ts">
import {defineComponent} from 'vue';

export default defineComponent({
    name: "Header"
});
</script>

<template>
    <header class="header">
        <a class="header__logo"
           href="https://vite.dev"
           target="_blank"
        >
            <img alt="Vite logo"
                 class="header__logo-icon"
                 src="/vite.svg"
            />
        </a>
        <a class="header__logo"
           href="https://github.com/web-fronttier"
           target="_blank"
        >
            <img alt="FrontTier logo"
                 class="header__logo-icon"
                 src="/fronttier.png"
            />
        </a>
        <a class="header__logo"
           href="https://vuejs.org/"
           target="_blank"
        >
            <img alt="Vue logo"
                 class="header__logo-icon"
                 src="/vue.svg"
            />
        </a>
    </header>
</template>

<style scoped>
.header {
    position: fixed;
    top: 0;
    left: 0;
    display: flex;
    gap: 16px;
    width: 100%;
    padding: 16px;
    box-shadow: 0 0 10px black;
    background: white;
}

.header__logo {
    display: flex;
}

.header__logo-icon {
    max-height: 32px;
    height: 100%;
    max-width: 32px;
    width: 100%;
}
</style>