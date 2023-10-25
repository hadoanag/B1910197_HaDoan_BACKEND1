<template>
    <div v-if="contact" class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm
            :contact="contact"
            @submit:contact="addContact"
            @delete:contact="resetContact"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false
        },
        message: "",
    };
  },
    methods: {
        async addContact(data) {
            try {
                 console.log("okkk")
                await ContactService.create(data);
                console.log("ok")
                this.message = "Liên hệ được thêm thành công.";
            } catch (error) {
                console.log(error);
            }
    
        },

        resetContact() {
            alert("reset");
        },
    },

    created() {
        this.message = "";
    },
};
</script>