<script setup lang="ts">
import { useTodoStore } from '@/stores/todo';
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue'

const actuals = [1, 1.5, 2, 4, 8]

const props = defineProps<{ id: number; actual: number | undefined }>()

const todoStore = useTodoStore()

function updateActual(newEstimate: number) {
    todoStore.updateActual(
        props.id,
        newEstimate
    )
}

</script>

<template>
    <td
        class="relative border border-table-border text-white text-sm font-medium hover:outline-2 hover:outline-blue-500 hover:rounded-md">
        <Menu as="div" class="relative text-sm font-medium">
            <MenuButton as="template">
                <button class="py-3 w-full" :class="{ 'py-6': !props.actual }">
                    {{ props.actual ? `${props.actual} SP` : '' }}
                </button>
            </MenuButton>
            <Transition enter-active-class="transition duration-100 ease-out"
                enter-from-class="transform scale-95 opacity-0" enter-to-class="transform scale-100 opacity-100"
                leave-active-class="transition duration-75 ease-in" leave-from-class="transform scale-100 opacity-100"
                leave-to-class="transform scale-95 opacity-0">
                <MenuItems
                    class="absolute z-50 right-0 mt-2 w-16 origin-top-right divide-y divide-gray-100 rounded-md bg-white shadow-lg ring-1 ring-black/5 focus:outline-none">
                    <div class="px-1 py-1">
                        <MenuItem v-slot="{ active }" v-for="actual of actuals" :key="actual">
                        <button :class="[
                            active ? 'bg-blue-500 text-white' : 'text-gray-900',
                            'group flex w-full items-center rounded-md px-2 py-2 text-sm',
                        ]" @click="updateActual(actual)">
                            {{ actual }}
                        </button>
                        </MenuItem>

                    </div>
                </MenuItems>
            </Transition>
        </Menu>
    </td>
</template>