<template>
    <ion-page>
        <ion-header>
            <ion-toolbar color="primary">
                <ion-title>Login</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content :fullscreen="true">
            <ion-header collapse="condense">
                <ion-toolbar>
                    <ion-title size="large">Login</ion-title>
                </ion-toolbar>
            </ion-header>

            <ion-card>
                <ion-card-header>
                    <ion-card-title class="text-center">Toko okoT</ion-card-title>
                </ion-card-header>
                <ion-card-content>
                    <ion-input label="Email" label-placement="floating" placeholder="Masukkan E-mail"
                        fill="solid"></ion-input>
                    <ion-input label="Password" label-placement="floating" placeholder="Masukkan Password"
                        fill="solid"></ion-input>

                    <div class="text-center">
                        <ion-button @click="login" size="default">Masuk</ion-button>
                    </div>
                </ion-card-content>
            </ion-card>

        </ion-content>
    </ion-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { axios } from "../../services/axios";
import { token, user, TUser } from "../../services/user";
import { useRouter } from "vue-router";

const email = ref('')
const password = ref('')
const router = useRouter()

const login = () => {
    axios.post('login', {
        email: email.value,
        password: password.value
    }).then(result => {
        const data = result.data?.value
        const mess = result.data.mess
        const isError = result.data.isError

        if (isError) {
            return
        }

        user.value = result.data?.value
        token.value = result.data?.token

        router.replace('tabs/tab1')
    }).catch(error => {
        console.log(error)
    })
}
</script>