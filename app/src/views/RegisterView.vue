<template>
    <div>
        <section class="form-container" v-if="currentLanguage == 'English'">
            <form @submit.prevent="registerUser">
                <h3>register now</h3>
                <input v-model="name" type="text" required maxlength="20" name="name" placeholder="enter your name" class="box" @input="removeSpaces('name')">
                <input v-model="mail" type="email" required maxlength="50" name="email" placeholder="enter your email" class="box" @input="removeSpaces('mail')">
                <input v-model="phone" type="number" min="0" max="9999999999" @keypress="limitNumberLength($event)" placeholder="enter your phone number" required class="box" name="number">
                <input v-model="address" type="text" required maxlength="100" name="address" placeholder="enter your address" class="box" @input="removeSpaces('address')">
                <input v-model="password" type="password" required maxlength="20" name="pass" placeholder="enter your password" class="box" @input="removeSpaces('password')">
                <input v-model="confirmPassword" type="password" required maxlength="20" name="cpass" placeholder="confirm your password" class="box" @input="removeSpaces('confirmPassword')">
                <input type="submit" value="register now" class="btn" name="submit">
                <p>already have an account? <router-link to="/login">login now</router-link></p>
            </form>
        </section>
        <section class="form-container"  v-if="currentLanguage == 'Srpski'">
            <form @submit.prevent="registerUser">
                <h3>registrujte se</h3>
                <input v-model="name" type="text" required maxlength="20" name="name" placeholder="unesite Vaše ime" class="box" @input="removeSpaces('name')">
                <input v-model="mail" type="email" required maxlength="50" name="email" placeholder="unesite email" class="box" @input="removeSpaces('mail')">
                <input v-model="phone" type="number" min="0" max="9999999999" @keypress="limitNumberLength($event)" placeholder="unesite broj telefona" required class="box" name="number">
                <input v-model="address" type="text" required maxlength="100" name="address" placeholder="unesite adresu" class="box" @input="removeSpaces('address')">
                <input v-model="password" type="password" required maxlength="20" name="pass" placeholder="unesite lozinku" class="box" @input="removeSpaces('password')">
                <input v-model="confirmPassword" type="password" required maxlength="20" name="cpass" placeholder="potvrdite lozinku" class="box" @input="removeSpaces('confirmPassword')">
                <input type="submit" value="registrujte se" class="btn" name="submit">
                <p>već imate nalog? <router-link to="/login">ulogujte se</router-link></p>
            </form>
        </section>
    </div>
</template>

<script>
export default {
    name: 'RegisterView',
    data() {
        return {
            name: '',
            mail: '',
            phone: '',
            address: '',
            password: '',
            confirmPassword: '',
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
        limitNumberLength(event) {
            if (event.target.value.length >= 10) {
                event.preventDefault();
            }
        },
        registerUser() {
            // Check if passwords match
            if (this.password !== this.confirmPassword) {
                alert("Passwords do not match");
                return;
            }

            // Get the current users from localStorage
            let users = JSON.parse(localStorage.getItem('registeredUsers')) || [];

            // Check if the user already exists
            if (users.some(user => user.mail === this.mail)) {
                alert("User already exists with this email");
                return;
            }

            // Create a new user object
            let newUser = {
                name: this.name,
                mail: this.mail,
                phone: this.phone,
                address: this.address,
                password: this.password
            };

            // Add the new user to the array and update localStorage
            users.push(newUser);
            localStorage.setItem('registeredUsers', JSON.stringify(users));

            alert("Registration successful");
            this.$router.push('/login');
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
