<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue';
import Label from '@/components/ui/label/Label.vue';
import AppLayout from '@/layouts/AppLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';

interface Product {
    id: number;
    name: string;
    description: string;
    price: number;
}

const props = defineProps<{ product: Product }>();

const form = useForm({
    name: props.product.name,
    description: props.product.description,
    price: props.product.price,
});

const handleSubmit = () => {
    form.put(route('products.update', { product: props.product.id }));
};
</script>

<template>
    <Head title="Edit Product" />

    <AppLayout
        :breadcrumbs="[
            {
                title: 'Edit Product',
                href: `/products/${props.product.id}/edit`,
            },
        ]"
    >
        <div class="p-4">
            <form @submit.prevent="handleSubmit()" class="w-8/12 space-y-4">
                <div class="flex flex-col space-y-2">
                    <Label for="Product name">Name</Label>
                    <input type="text" placeholder="isikan sesuai keyakinan" class="rounded-sm px-2 py-0.5 text-black" v-model="form.name" />
                    <div class="text-sm text-red-500" v-if="form.errors.name">{{ form.errors.name }}</div>
                </div>
                <div class="flex flex-col space-y-2">
                    <Label for="Product description">Description</Label>
                    <input type="text" placeholder="isikan sesuai keyakinan" class="rounded-sm px-2 py-0.5 text-black" v-model="form.description" />
                    <div class="text-sm text-red-500" v-if="form.errors.description">{{ form.errors.description }}</div>
                </div>
                <div class="flex flex-col space-y-2">
                    <Label for="Product price">Price</Label>
                    <input type="number" placeholder="isikan sesuai keyakinan" class="rounded-sm px-2 py-0.5 text-black" v-model="form.price" />
                    <div class="text-sm text-red-500" v-if="form.errors.price">{{ form.errors.price }}</div>
                </div>
                <Button type="submit" :disabled="form.processing">Edit a Product</Button>
                <!-- disable button while processing to prevent multiple submissions -->
            </form>
        </div>
    </AppLayout>
</template>
