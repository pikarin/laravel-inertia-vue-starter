<script setup>
import BreezeButton from '@/Components/AppButton.vue'
import BreezeGuestLayout from '@/Layouts/Guest.vue'
import BreezeInput from '@/Components/AppInput.vue'
import BreezeLabel from '@/Components/AppLabel.vue'
import BreezeValidationErrors from '@/Components/ValidationErrors.vue'
import { Head, useForm } from '@inertiajs/inertia-vue3'

const props = defineProps({
    email: String,
    token: String,
})

const form = useForm({
    token: props.token,
    email: props.email,
    password: '',
    password_confirmation: '',
})

const submit = () => {
    form.post(route('password.update'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    })
}
</script>

<script>
export default {
    layout: BreezeGuestLayout,
}
</script>

<template>
    <Head title="Reset Password" />

    <BreezeValidationErrors class="mb-4" />

    <form @submit.prevent="submit">
        <div>
            <BreezeLabel for="email" value="Email" />
            <BreezeInput
                id="email"
                v-model="form.email"
                type="email"
                class="mt-1 block w-full"
                required
                autofocus
                autocomplete="username"
            />
        </div>

        <div class="mt-4">
            <BreezeLabel for="password" value="Password" />
            <BreezeInput
                id="password"
                v-model="form.password"
                type="password"
                class="mt-1 block w-full"
                required
                autocomplete="new-password"
            />
        </div>

        <div class="mt-4">
            <BreezeLabel for="password_confirmation" value="Confirm Password" />
            <BreezeInput
                id="password_confirmation"
                v-model="form.password_confirmation"
                type="password"
                class="mt-1 block w-full"
                required
                autocomplete="new-password"
            />
        </div>

        <div class="mt-4 flex items-center justify-end">
            <BreezeButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                Reset Password
            </BreezeButton>
        </div>
    </form>
</template>
