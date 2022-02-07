<template>
    <div class="container mx-auto mt-16 sm:px-6 lg:px-8">
        <form class="bg-green-500 rounded mx-auto px-6 py-6 w-1/2" @submit.prevent="login">
            <div class="flex flex-col mt-3">
                <label class="text-white text-xl" for="email">Email</label>
                <input v-model="form.email" class="px-2 py-1 rounded" placeholder="Email" type="email">
                <!--                <span v-if="errors.email" class="text-red-200 italic">{{ errors.email[0] }}</span>-->
            </div>
            <div class="flex flex-col mt-3">
                <label class="text-white text-xl" for="password">Password</label>
                <input v-model="form.password" class="px-2 py-1 rounded" placeholder="Password" type="password">
                <!--                <span v-if="errors.password" class="text-red-200 italic">{{ errors.password[0] }}</span>-->
            </div>
            <div class="text-center mt-3">
                <button type="submit">login</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            form: {
                email: '',
                password: '',
            }
        }
    },
    methods: {
        async login() {
            try {
                await this.$auth.loginWith('laravelSanctum', {
                    data: this.form
                })
            } catch (e) {
                console.log(e)
            }
        }
    }
}
</script>

<style scoped>

</style>
