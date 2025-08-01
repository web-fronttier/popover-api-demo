<script lang="ts" setup>
import {onBeforeUnmount, onMounted, ref} from 'vue';
import tippy, {type Instance, type Props} from 'tippy.js';

const props = defineProps<{
    content: string,
    type?: 'click' | 'focus',
}>();

const triggerRef = ref<HTMLElement | null>(null);
let tip: Instance<Props> | null = null;

onMounted(() => {
    if (triggerRef.value) {
        const tippyProps: Record<string, any> = {
            content: props.content,
            placement: 'top',
        };
        if (props.type) {
            tippyProps.trigger = props.type;
        }

        tip = tippy(triggerRef.value, tippyProps);
    }
});

onBeforeUnmount(() => {
    tip?.destroy();
});
</script>
<template>
    <a ref="triggerRef"
       class="tippy-tooltip"
       href="#"
    >Tooltip on {{ props.type ?? 'hover' }}</a>
</template>
<style lang="scss" scoped>
.tippy-tooltip {
    cursor: pointer;
    color: #336dcc;
    text-decoration: underline dotted;

    &:focus-visible {
        outline: 2px solid black;
        outline-offset: 2px;
        border-radius: 2px;
    }
}
</style>
