<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Carousel, CarouselContent, CarouselItem, CarouselNext, CarouselPrevious } from '@/components/ui/carousel'
import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'

import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";

const greetMsg = ref("");
const name = ref("");

async function greet() {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  greetMsg.value = await invoke("greet", { name: name.value });
}

</script>

<template>


  <section class="bg-white dark:bg-gray-900">
    <div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:py-16 lg:px-12">
        
        <h1 class="mb-4 text-4xl font-extrabold tracking-tight leading-none text-gray-900 md:text-5xl lg:text-6xl dark:text-white">Tauri Shadcn-vue Template</h1>
        <p class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 xl:px-48 dark:text-gray-400">This templated is intended to jump start your cross platform desktop app development. <br> 
            Recommended IDE setup: VS Code + Volar + Tauri + rust-analyzer.
        
        </p>
        
        <div class="flex flex-col mb-8 lg:mb-16 space-y-4 sm:flex-row sm:justify-center sm:space-y-0 sm:space-x-4">
            
                <form class="flex w-full max-w-sm items-center gap-1.5"  @submit.prevent="greet">
                    <Input   v-model="name"  placeholder="Enter your name..." />
                    <Button type="submit" @submit.prevent="greet">
                     Hello
                    </Button>
                </form>    
        </div>
        <p class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 xl:px-48 dark:text-gray-400"> {{ greetMsg }} , below isa  quick example of cool things you can build quickly</p>
        <div class="flex flex-col mb-8 lg:mb-16 space-y-4 sm:flex-row sm:justify-center sm:space-y-0 sm:space-x-4">
            <Carousel class="relative w-full max-w-xs">
                    <CarouselContent>
                    <CarouselItem v-for="(_, index) in 5" :key="index">
                        <div class="p-1">
                        <Card>
                            <CardContent class="flex aspect-square items-center justify-center p-6">
                            <span class="text-4xl font-semibold">{{ index + 1 }}</span>
                            </CardContent>
                        </Card>
                        </div>
                    </CarouselItem>
                    </CarouselContent>
                    <CarouselPrevious />
                    <CarouselNext />
                </Carousel>
        </div>    
    </div>
</section>


</template>