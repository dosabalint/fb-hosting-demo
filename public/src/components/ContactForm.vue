<template>
    <form action="">
        <div class="text-center">
            <h1>Írj nekünk bátran!</h1>
        </div>
    
        <div class="form-group">
            <label for="nameInput">Név</label>
            <input class="form-control" id="nameInput" placeholder="Name" required v-model="name">
        </div>
    
        <div class="form-group">
            <label for="emailInput">Email</label>
            <input type="email" class="form-control" id="emailInput" placeholder="name@example.com" required v-model="email">
        </div>
    
        <div class="form-group">
            <label for="subjectInput">Tárgy</label>
            <input class="form-control" id="subjectInput" required v-model="subject">
        </div>
    
        <div class="form-group">
            <label for="messageTextarea">Üzenet</label>
            <textarea class="form-control" id="messageTextarea" rows="3" v-model="message" required></textarea>
        </div>
    
        <button type="submit" class="btn mb-4" :class="{'btn-primary': isValid, 'btn-secondary': !isValid}" :disabled="!isValid" @click="submit">Küldés</button>
    
        <div class="alert alert-success" role="alert" v-if="success">
            Sikeresen beküldted az üzenetet!
        </div>

        <div class="alert alert-danger" role="alert" v-if="success === false">
            A beküldés valamiért sikertelen volt!
        </div>
    </form>
</template>

<script>
    import axios from 'axios';
    
    const fbUrl = "https://my-fb-hosting-demo.firebaseio.com/contactMessages.json";
    
    export default {
        data() {
            return {
                name: "Demo Dénes",
                email: "demo.denes@gmail.com",
                subject: "Teszt üzenet",
                message: "Lorem ipsum dolor et samet.",
                success: null
            };
        },
        computed: {
            isValid() {
                return !!this.name &&
                    /@.*?\./.test(this.email) &&
                    !!this.subject &&
                    !!this.message;
            },
            formData() {
                return {
                    name: this.name,
                    email: this.email,
                    subject: this.subject,
                    message: this.message
                }
            }
        },
        methods: {
            submit(event) {
                if (!this.isValid) return;
    
                event.preventDefault();
                
                this.success = null;
                axios.post(fbUrl, this.formData)
                    .then(response => {
                        this.success = true;
                        this.clear();
                    })
                    .catch(error => {
                        this.success = false;
                    });
            },
            clear() {
                this.name = '';
                this.email = '';
                this.subject = '';
                this.message = '';
            }
        }
    };
</script>
