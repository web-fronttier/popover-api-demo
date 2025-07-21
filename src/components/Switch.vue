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
    <label :class="{ 'toggle--checked': checked }"
           class="toggle"
           @click="toggle"
    >
        <span :aria-checked="checked"
              class="toggle__q"
              role="checkbox"
              tabindex="0"
              @keydown.space.prevent="toggle"
              @keydown.enter.prevent="toggle"
        >
            <span class="toggle__track"></span>
            <span class="toggle__thumb"></span>
        </span>
        <span>Just test for interaction</span>
    </label>
</template>
<style lang="scss" scoped>
.toggle {
    cursor: pointer;
    display: inline-flex;
    gap: 16px;

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

.toggle__q {
    display: inline-flex;
    cursor: pointer;
    align-items: center;
    width: 44px;
    height: 24px;
    position: relative;
    user-select: none;
    outline: none;
}

.toggle:focus {
    outline: 2px solid #42b98333;
    border-radius: 12px;
}
</style>