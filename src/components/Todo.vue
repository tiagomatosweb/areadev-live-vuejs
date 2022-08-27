<template>
    <div
        class="flex items-center bg-white rounded p-2 text-sm text-gray-600 cursor-pointer"
        @click="onToggle"
    >
        <CheckIcon
            v-if="todo.is_done"
            class="mr-1"
        />

        <div>
            {{ todo.title }}
        </div>

        <a
            href=""
            class="ml-auto text-xs text-red-400"
            @click.stop.prevent="onDelete"
        >
            Remover
        </a>
    </div>
</template>

<script>
import CheckIcon from './CheckIcon.vue'

export default {
    components: {
        CheckIcon
    },

    props: {
        todo: {
            type: Object,
            default: () => ({})
        },
    },

    methods: {
        onToggle() {
            this.$emit('onClick', this.todo)
        },

        onDelete() {
            this.$emit('onRemove', this.todo)
        }
    }
}
</script>
