<script lang="ts">
import {defineComponent} from 'vue'

export default defineComponent({
    name: 'Switch',
    data() {
        return {
            checked: false as boolean
        }
    },
    methods: {
        toggle() {
            this.checked = !this.checked
        }
    }
})
</script>
<template>
    <div :aria-checked="checked"
         :class="{ 'toggle--checked': checked }"
         class="toggle"
         role="checkbox"
         tabindex="0"
         @click="toggle"
         @keydown.space.prevent="toggle"
         @keydown.enter.prevent="toggle"
    >
        <div class="toggle__track"></div>
        <div class="toggle__thumb"></div>
    </div>
</template>
<style lang="scss" scoped>
.toggle {
    display: inline-flex;
    cursor: pointer;
    align-items: center;
    width: 44px;
    height: 24px;
    position: relative;
    user-select: none;
    outline: none;

    &__track {
        width: 100%;
        height: 100%;
        background: #ccc;
        border-radius: 12px;
        transition: background 0.2s;
    }

    &__thumb {
        position: absolute;
        top: 2px;
        left: 2px;
        width: 20px;
        height: 20px;
        background: #fff;
        border-radius: 50%;
        box-shadow: 0 1px 4px rgba(0, 0, 0, 0.16);
        transition: left 0.2s, background 0.2s;
    }

    &--checked &__track {
        background: #42b983;
    }

    &--checked &__thumb {
        left: 22px;
        background: #fff;
    }
}

.toggle:focus {
    outline: 2px solid #42b98333;
    border-radius: 12px;
}
</style>