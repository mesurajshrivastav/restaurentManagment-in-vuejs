<template>
<HeaderPage />
<h2>Welcome to update restaurent page</h2>
<form class="resAdd">
    <input type="text" name="name" placeholder="Enter Name" v-model="Restaurent.name" />
    <input type="text" name="contact" placeholder="Enter Contact" v-model="Restaurent.contact" />
    <input type="text" name="address" placeholder="Enter Address" v-model="Restaurent.address" />
    <button type="button" v-on:click="updateRestaurent">Update Restaurent</button>
</form>
</template>

<script>
import HeaderPage from "./HeaderPage.vue"
import axios from "axios";
export default {
    name: "UpdateRestaurent",
    components: {
        HeaderPage
    },
    data() {
        return {
            Restaurent: {
                name: "",
                contact: "",
                address: "",
            }
        }
    },
    methods: {
       async updateRestaurent() {
            let result = await axios.put(`http://localhost:3000/restaurent/${this.$route.params.id}`, {
                name: this.Restaurent.name,
                contact: this.Restaurent.contact,
                address: this.Restaurent.address,
            })
            console.log(result);

            if (result.status == 200) {
                // localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({
                    name: 'HomePage'
                })
            }

        }
    },
   async mounted() {
        let user = localStorage.getItem("user-info");

        if (!user) {
            this.$router.push({
                name: "SignUp",
            });
        }

        let result = await axios.get(`http://localhost:3000/restaurent/${this.$route.params.id}`)
        this.Restaurent = result.data;
        console.log(result);
        // console.log(this.$route.params.id) // getting id 
    }
}
</script>
