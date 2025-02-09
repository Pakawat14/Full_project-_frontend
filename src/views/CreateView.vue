<template>
    <div class="q-gutter-md" style="max-width: 400px">
        <q-form @submit="onSubmit" class="q-gutter-md">

            <q-input v-model="first_name" label="ชื่อจริง" />
            <q-input v-model="last_name" label="นามสกุล" />
            <q-input v-model="email" label="email" />
            <q-input v-model="address" label="ที่อยู่" />
            <q-input v-model="phone_number" label="เบอร์โทรศัพท์"  />
            <q-btn type="submit" label="บันทึก" color="primary" />
        </q-form>

    </div>
</template>

<script setup>
import { ref } from 'vue'
import router from '../router'

const first_name = ref('')
const last_name = ref('')
const email = ref('')
const address = ref('')
const phone_number = ref('')

const onSubmit = async () => {
    const myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");

    const raw = JSON.stringify({
        "first_name": first_name.value,
        "last_name": last_name.value,
        "address": address.value,
        "email": email.value,
        "phone_number": phone_number.value
    });

    const requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: raw,
        redirect: "follow"
    };

    fetch("http://localhost:8800/api/v1/customers", requestOptions)
        .then((response) => response.json())
        .then((result) => {
            alert(result.message);
            if (result.status === "ok") {
                router.push("/");
            }
        })
        .catch((error) => console.error(error));
}

</script>
