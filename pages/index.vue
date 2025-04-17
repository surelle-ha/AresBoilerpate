<template>
    <div class="container mx-auto text-gray-300">
        <div class="flex flex-col items-center">
            <div class="w-full flex flex-wrap space-x-8 justify-center mt-12">
                <a target="_blank" class="flex items-center" href="https://nuxt.com/">
                    <img class="w-44" src="https://nuxt.com/assets/design-kit/icon-green.svg" alt="nuxt3">
                </a>
                <a target="_blank" class="flex items-center" href="https://tauri.app/">
                    <img class="w-28"
                        src="https://raw.githubusercontent.com/github/explore/70444453f0d8b1143dca3a7b273119ef88bd4399/topics/tauri/tauri.png"
                        alt="tauri app">
                </a>
                <a target="_blank" class="flex items-center" href="https://tailwindcss.com/">
                    <img class="w-44"
                        src="https://upload.wikimedia.org/wikipedia/commons/thumb/archive/d/d5/20230715030041%21Tailwind_CSS_Logo.svg/120px-Tailwind_CSS_Logo.svg.png"
                        alt="tailwind">
                </a>
            </div>
            <p class="text-2xl">
                NuxtJS3 - Tauri2 - TailwindCSS
            </p>
            <p class="text-gray-400 mb-4">by <a href="https://github.com/surelle-ha" target="_blank"
                    class="underline">Surelle-ha</a></p>
            <p class="text-gray-400">App name: {{ appName }}</p>
            <p class="text-gray-400">App version: {{ appVersion }}</p>
            <p class="text-gray-400">Tauri version: {{ tauriVersion }}</p>

            <div class="w-full flex flex-col items-center mt-8">
                <UFormField label="What is your name?" :error="errorMessage" required>
                    <UInput v-model="demoName" placeholder="Enter your name" icon="i-lucide-pen" />
                </UFormField>
                <UButton class="mt-4 cursor-pointer" label="Greet" variant="outline" @click="validateAndShowToast" />
            </div>
        </div>

    </div>
</template>

<script setup lang="ts">
import { getTauriVersion, getVersion, getName } from '@tauri-apps/api/app';

const toast = useToast();
const appName = await getName();
const appVersion = await getVersion();
const tauriVersion = await getTauriVersion();

const demoName = ref('');
const errorMessage = ref('');

const validateAndShowToast = () => {
    if (!demoName.value.trim()) {
        errorMessage.value = 'Name cannot be empty.';
        return;
    }
    errorMessage.value = '';
    toast.add({
        title: 'Hello ' + demoName.value,
        description: 'This is a demo of the Tauri app with Nuxt3 and TailwindCSS.'
    });
}
</script>