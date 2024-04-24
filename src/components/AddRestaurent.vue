<template>
<HeaderPage />
<h2>Welcome to add restauren page</h2>
<form class="resAdd">
    <input type="text" name="name" placeholder="Enter Name " v-model="Restaurent.name" />
    <input type="text" name="contact" placeholder="Enter Contact" v-model="Restaurent.contact" />
    <input type="text" name="address" placeholder="Enter Address" v-model="Restaurent.address" />
    <button type="button" v-on:click="addRestaurent">Add New Restaurent</button>
</form>
</template>

<script>
import HeaderPage from "./HeaderPage.vue";
import axios from "axios";

export default {
    name: "AddRestaurent",
    data() {
        return {
            Restaurent: {
                name: "",
                contact: "",
                address: "",
            }
        }
    },
    components: {
        HeaderPage,
    },
    methods: {
        async addRestaurent() {
            let result = await axios.post("http://localhost:3000/restaurent", {
                name: this.Restaurent.name,
                contact: this.Restaurent.contact,
                address: this.Restaurent.address,
            })
            console.log(result);

            if (result.status == 201) {
                // localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({
                    name: 'HomePage'
                })
            }

        }
    }
}
</script>

<style>
.resAdd {
    display: flex;
    flex-direction: column;
    width: 400px;
    margin: auto;
}

.resAdd input {
    padding: 5px;
    margin: 5px;
}

.resAdd button {
    width: 390px;
    padding: 5px;
    margin: 5px;
}
</style>
