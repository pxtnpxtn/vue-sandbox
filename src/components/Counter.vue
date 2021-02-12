<script lang="ts">
import { computed, defineComponent, onBeforeUpdate, onMounted, onUnmounted, onUpdated, reactive, ref, watch } from "vue";

export default defineComponent ({
    name: "Counter",
    props: {
        emoji: { type: String, default: '🔥' }
    },
    // setup is called before the component is created, and after props have been resolved.
    // Setup takes (props, context) as possible arguments.
    setup(props) {

        // Add before to any of them.
        onMounted(() => console.log('Counter component has been mounted'));
        onBeforeUpdate(() => console.log('Counter is about to be updated'));
        onUpdated(() => console.log('Counter has been updated'));
        onUnmounted(() => console.log('Counter has been unmounted'));
        // onActivated, onDeactivated, onErrorCaptured, onRenderTracked, onRenderTriggered

        const counterReactive = reactive({ anotherCount: 0 });
        const counter = ref(0);
        const increment = () => counter.value++;

        // watch(reactive reference, (current, previous)). Can also just be (reactive reference, current).
        watch(counter, (current, previous) => {
            console.log('watch-->', current, previous);

            if (current === 3) console.log('clicked 3 times')
        })

        const arrayOfEmojis = computed(() => {
            return Array.from(new Array(counter.value), () => props.emoji).join(' ')
            // return 'Hello'
        })

        // Anything returned will be reactive and usable in template
        // Variables and functions need to be returned
        return { counter, increment, arrayOfEmojis, counterReactive }
    }
});
</script>

<template>
  <button @click="increment">Increase</button>
  <div>{{ counter }} </div>
  <div>{{ counterReactive }} </div>
  <div>{{ arrayOfEmojis }} </div>
</template>

<style scoped lang="scss">

</style>