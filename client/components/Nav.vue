<template>
    <div class="bg-green-500 text-white text-md">
        <nav class="container flex justify-between items-center mx-auto py-5">
            <span class="font-semibold text-2xl">Friendzy</span>
            <div>
                <span class="hover:underline"><nuxt-link to="/">Home</nuxt-link></span>
                <span class="hover:underline"><nuxt-link to="/dashboard">Dashboard</nuxt-link></span>
                <span class="hover:underline"><nuxt-link to="/auth/login">Login</nuxt-link></span>
                <span class="hover:underline"><nuxt-link to="/auth/register">Register</nuxt-link></span>
            </div>
        </nav>
    </div>
</template>
