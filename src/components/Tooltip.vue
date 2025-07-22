<script lang="ts">
import {defineComponent, onBeforeUnmount, onMounted, ref} from 'vue';
import type {Instance, Props} from 'tippy.js';
import tippy from 'tippy.js';

export default defineComponent({
    name: 'Tooltip',
    props: {
        content: {
            type: String,
            required: true
        }
    },
    setup(props) {
        const triggerRef = ref<HTMLElement | null>(null);
        let tip: Instance<Props> | null = null;

        onMounted(() => {
            if (triggerRef.value) {
                tip = tippy(triggerRef.value, {
                    content: props.content,
                    placement: 'top',
                });
            }
        })

        onBeforeUnmount(() => {
            if (tip) {
                tip.destroy();
            }
        })

        return {triggerRef}
    }
})
</script>
<template>
    <span ref="triggerRef" class="tippy-tooltip__trigger">
        <slot>Tooltip on hover</slot>
    </span>
</template>
<style lang="scss" scoped>
.tippy-tooltip__trigger {
    cursor: pointer;
    color: #336dcc;
    text-decoration: underline dotted;
}
</style>
