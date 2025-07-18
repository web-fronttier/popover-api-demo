<script lang="ts">
import {defineComponent} from 'vue'

export default defineComponent({
    name: 'DialogWindow',
    props: {
        isModal: {
            type: Boolean,
            default: true
        }
    },
    data() {
        return {
            showDialog: false as boolean,
            originalBodyOverflow: '' as string // сохраняем исходное состояние
        }
    },
    methods: {
        openDialog() {
            this.showDialog = true;
            if (this.isModal) {
                this.originalBodyOverflow = document.body.style.overflow;
                document.body.style.overflow = 'hidden';
                window.addEventListener('keydown', this.handleKeydown);
            }
        },
        closeDialog() {
            this.showDialog = false;
            if (this.isModal) {
                document.body.style.overflow = this.originalBodyOverflow || '';
                window.removeEventListener('keydown', this.handleKeydown);
            }
        },
        handleBackdropClick(event: MouseEvent) {
            if (this.isModal && (event.target === event.currentTarget)) {
                this.closeDialog();
            }
        },
        handleKeydown(event: KeyboardEvent) {
            if (event.key === 'Escape' && this.showDialog) {
                this.closeDialog();
            }
        }
    },
    beforeUnmount() {
        if (this.isModal) {
            document.body.style.overflow = this.originalBodyOverflow || '';
            window.removeEventListener('keydown', this.handleKeydown);
        }
    }
});
</script>

<template>
    <!-- Модальное — поверх, с backdrop. Немодальное — просто плавающий блок в потоке -->
    <div v-if="showDialog"
         :class="{'dialog--modal': isModal}"
         class="dialog"
         @click="handleBackdropClick"
    >
        <div class="dialog__window">
            <h2>Это {{ isModal ? 'модальное' : 'диалоговое, не модальное' }} окно!</h2>
            <button class="dialog__close" @click="closeDialog">x</button>
        </div>
    </div>
    <button @click="openDialog">{{ isModal ? 'Модальное' : 'Диалоговое' }} окно</button>
</template>

<style lang="scss" scoped>
.dialog {
    --dialog-window-bg-color: lightblue;

    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    align-items: flex-start;
    justify-content: flex-start;
    max-width: max-content;
    width: auto;
    max-height: max-content;
    height: auto;
    margin: auto;
    padding: 0;
    background: transparent;
    z-index: auto;
    background: none;

    &--modal {
        --dialog-window-bg-color: white;

        align-items: center;
        justify-content: center;
        max-width: unset;
        width: 100%;
        max-height: unset;
        height: 100%;
        inset: 0;
        background: rgba(0, 0, 0, 0.45);
        z-index: 100;
    }
}

.dialog__window {
    position: relative;
    padding: 2rem 1.5rem;
    min-width: 250px;
    border-radius: 10px;
    background-color: var(--dialog-window-bg-color, lightblue);
    box-shadow: 0 2px 16px rgba(0, 0, 0, 0.10);
    margin: 1.5rem 0;
}

/* Немодальный: просто плавающий div без фона и фиксированности */
.dialog__close {
    position: absolute;
    top: -16px;
    right: -16px;
    height: 32px;
    width: 32px;
    font-size: 20px;
    padding: 0;
    border: 1px solid black;
    border-radius: 100px;
    background: white;
    will-change: background;
    transition: background-color .2s;

    &:focus,
    &:hover {
        background: lightgray;
    }
}
</style>