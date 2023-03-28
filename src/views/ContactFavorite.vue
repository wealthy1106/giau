<template>
    <div class="page">
        <ContactForm @submit:contact="createContact" @createContact:contact="createContact" />
        <p>{{ message }}</p>
    </div>
    <H4 style="text-align: center;">Danh sách liên hệ yêu thích</H4>
    <table class="table table-bordered">
        <thead>
            <tr>
                <th scope="col">Tên</th>
                <th scope="col">Email</th>
                <th scope="col">Số điện thoại</th>
                <th scope="col">Địa chỉ</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="user in contacts">
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>
                <td>{{ user.phone }}</td>
                <td>{{ user.adress }}</td>
            </tr>
        </tbody>
    </table>
</template>
<script>
import ContactService from "@/services/contact.service";
import ContactList from "@/components/ContactList.vue";
import axios from 'axios';
export default {

    data() {
        return {
            contacts: [],
        }
    },
    mounted() {
        axios.get('http://localhost:3000/api/contact/favorite/')
            .then((response) => {
                console.log(response.data);
                this.contacts = response.data;
            })
            .catch((error) => {
                console.log(error);
            });
    },
}
</script>