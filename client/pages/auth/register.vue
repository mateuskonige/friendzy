<template>
    <div class="container mx-auto mt-16 sm:px-6 lg:px-8">
        <form class="bg-green-500 rounded mx-auto px-6 py-6 w-1/2" @submit.prevent="register">
            <div class="flex flex-col">
                <label class="text-white text-xl" for="name">Name</label>
                <input v-model="form.name" class="px-2 py-1 rounded" placeholder="Name" type="text">
                <!--                <span v-if="errors.name" class="text-red-200 italic">{{ errors.name[0] }}</span>-->
            </div>
            <div class="flex flex-col mt-3">
                <label class="text-white text-xl" for="username">Username</label>
                <input v-model="form.username" class="px-2 py-1 rounded" placeholder="Username" type="text">
                <!--                <span v-if="errors.username" class="text-red-200 italic">{{ errors.username[0] }}</span>-->
            </div>
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
            <div class="flex flex-col mt-3">
                <label class="text-white text-xl" for="password_confirmation">Confirm Password</label>
                <input v-model="form.password_confirmation" class="px-2 py-1 rounded" placeholder="Confirm Password"
                       type="password">
            </div>
            <div class="text-center mt-3">
                <button type="submit">Register</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            form: {
                name: '',
                username: '',
                email: '',
                password: '',
                password_confirmation: '',
            },
            errors: null,
        }
    },
    methods: {
        async register() {
            try {
                let errors = [];
                await this.$axios.$get('sanctum/csrf-cookie')
                await this.$axios.$post('/register', this.form)
                    .then((res) => {
                        console.log(res)
                    })
                    .catch((err) => {
                        if (err.response.status == 422) {
                            errors = err.response.data.errors
                        }
                    })
                this.errors = errors;
                
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
