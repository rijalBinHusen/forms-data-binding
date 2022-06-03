<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" v-model="email" required />

        <label>Password:</label>
        <input type="password" v-model="password" required />
        <div v-if="passwordError" class="error"> {{ passwordError }} </div>

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web developer</option>
            <option value="designer">Web designer</option>
        </select>

        <label for="skills">Skill</label>
        <input type="text" id="skills" v-model="tempSkill" @keyup.alt="addSkill">
        <div @click="deleteSkill(skill)" v-for="skill in skills" :key="skill" class="pill">
            {{ skill }}
        </div>

        <div class="terms">
            <input type="checkbox" v-model="terms" id="terms" required />
            <label for="terms">Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an account</button>
        </div>

    </form>
</template>

<script>
export default {
    name: "SignupForm",
    data() {
        return {
            email: "",
            password: "",
            role: "designer",
            terms: false,
            tempSkill: "",
            skills: [],
            passwordError: "",
        }
    },
    methods: {
        addSkill(e) {
            if(e.key === "," && this.tempSkill){
                // if the skill already include in skills
                if(!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                    this.tempSkill = ""
            }
        },
        deleteSkill(e) {
            this.skills = this.skills.filter((val) => val !== e)
        },
        handleSubmit() {
            // console.log("SignupForm")
            // validate password
            this.passwordError = this.password.length > 5 
                                    ? '' 
                                    : "Password must be at least 6 chars long"
            if(!this.passwordError) {
                console.log("email", this.email)
                console.log("password", this.password)
                console.log("role", this.role)
                console.log("skills", this.skills)
            }
        }
    },
}
</script>

<style scoped>
form {
    max-width: 500px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px
}

label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input, select {
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"] {
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.pill {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}

button {
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}

.submit {
    text-align: center;
}

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}

</style>