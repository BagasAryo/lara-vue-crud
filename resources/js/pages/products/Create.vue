<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue';
import Label from '@/components/ui/label/Label.vue';
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head, useForm } from '@inertiajs/vue3';

const breadcrumbs: BreadcrumbItem[] = [
    {
        title: 'Create A Product',
        href: '/products/create',
    },
];

const form = useForm({
    name: '',
    description: '',
    price: 0,
});

const handleSubmit = () => {
    form.post(route('products.store'), {
        onSuccess: () => {
            form.reset();
        },
    });
}

defineProps<{
    name?: string;
}>();
</script>

<template>
    <Head title="Create Product" />

    <AppLayout :breadcrumbs="breadcrumbs">
        <div class="p-4">
            <form @submit.prevent="handleSubmit()" class="w-8/12 space-y-4">
                <div class="flex space-y-2 flex-col">
                    <Label for="Product name">Name</Label>
                    <input 
                        type="text" 
                        placeholder="isikan sesuai keyakinan" 
                        class="px-2 py-0.5 rounded-sm text-black" 
                        v-model="form.name"
                    />
                    <div class="text-red-500 text-sm" v-if="form.errors.name">{{ form.errors.name }}</div>
                </div>
                <div class="flex space-y-2 flex-col">
                    <Label for="Product description">Description</Label>
                    <input 
                        type="text" 
                        placeholder="isikan sesuai keyakinan" 
                        class="px-2 py-0.5 rounded-sm text-black" 
                        v-model="form.description"
                    />
                    <div class="text-red-500 text-sm" v-if="form.errors.description">{{ form.errors.description }}</div>
                </div>
                <div class="flex space-y-2 flex-col">
                    <Label for="Product price">Price</Label>
                    <input 
                        type="number" 
                        placeholder="isikan sesuai keyakinan" 
                        class="px-2 py-0.5 rounded-sm text-black" 
                        v-model="form.price"
                    />
                    <div class="text-red-500 text-sm" v-if="form.errors.price">{{ form.errors.price }}</div>
                </div>
                <Button>Add a Product</Button>
            </form>
        </div>
    </AppLayout>
</template>
