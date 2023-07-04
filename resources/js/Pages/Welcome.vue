<script setup>
import {useForm} from "laravel-precognition-vue-inertia";

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});

let form = useForm('post', route('testIssue'), {
    email: null,
    phone: null
})

const submit = () => {
    console.log("E-Mail Valid: " + form.valid("email"), "E-Mail Invalid: " + form.invalid("email"))
    console.log("Phone Valid: " + form.valid("phone"), "Phone Invalid: " + form.invalid("phone"))
    form.submit({
        preserveScroll: true,
        onSuccess: () => form.reset(),
    });
};
</script>

<template>
    <form @submit.prevent="submit" class="grid grid-cols-1 max-w-lg mx-auto mt-20 space-y-3">
        <input placeholder="E-Mail*" class="form-input rounded-lg" v-model="form.email" type="email" @change="form.validate('email')">
        <input placeholder="Phone*" class="form-input rounded-lg" v-model="form.phone" type="tel" @change="form.validate('phone')">
        <button class="border-2 border-green-500 bg-green-500 text-white rounded-md py-2" type="submit">Submit</button>
    </form>
</template>
