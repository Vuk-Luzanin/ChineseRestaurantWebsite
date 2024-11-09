<template>
    <div>   
        <section class="form-container" v-if="currentLanguage == 'English'">
            <form @submit.prevent="loginUser">
                <h3>login now</h3>
                <input v-model="mail" type="email" required maxlength="50" name="email" placeholder="enter your email" class="box" @input="removeSpaces('mail')">
                <input v-model="password" type="password" required maxlength="20" name="pass" placeholder="enter your password" class="box" @input="removeSpaces('password')">
                <input type="submit" value="login now" class="btn" name="submit">
                <p>don't have an account? <router-link to="/register">register now</router-link></p>
            </form>
        </section>
        <section class="form-container" v-if="currentLanguage == 'Srpski'">
            <form @submit.prevent="loginUser">
                <h3>Ulogujte se</h3>
                <input v-model="mail" type="email" required maxlength="50" name="email" placeholder="unesite email" class="box" @input="removeSpaces('mail')">
                <input v-model="password" type="password" required maxlength="20" name="pass" placeholder="unessite lozinku" class="box" @input="removeSpaces('password')">
                <input type="submit" value="ulogujte se" class="btn" name="submit">
                <p>Nemate profil? <router-link to="/register">registrujte se</router-link></p>
            </form>
        </section>
    </div>
</template>

<script>
export default {
    name: 'LoginView',
    data() {
        return {
            mail: '',
            password: '',
            currentLanguage: 'English',
        }
    },
    created() {
        // Postavljanje trenutnog jezika na osnovu lokalnog skladišta
      const savedLanguage = localStorage.getItem('language');
      if (savedLanguage === 'sr') {
         this.currentLanguage = 'Srpski';
      } else {
         this.currentLanguage = 'English';
      }
    },
    methods: {
        removeSpaces(field) {
            this[field] = this[field].replace(/\s/g, '');
        },
        loginUser() {
            // Get the current users from localStorage
            let users = JSON.parse(localStorage.getItem('registeredUsers')) || [];

            // Check if the user exists and password matches
            let user = users.find(user => user.mail === this.mail && user.password === this.password);

            if (user) {
                // Store the logged-in user in localStorage
                localStorage.setItem('user', JSON.stringify(user));
                alert("Login successful");
                this.$router.push('/');
            } else {
                alert("Invalid email or password");
            }
        }
    }
}
</script>

<style>
/* Add necessary styles */
.form-container {
    max-width: 500px;
    margin: 0 auto;
    padding: 2rem;
    border: 1px solid #ccc;
    border-radius: 5px;
    background: #fff;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.form-container form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.form-container .box {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.form-container .btn {
    padding: 0.5rem;
    background: #3498db;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.form-container .btn:hover {
    background: #2980b9;
}
</style>
