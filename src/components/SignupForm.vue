<template>
    <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" required v-model="email" >
        <label>Passowrd:</label>
        <input type="password" required v-model="password" >
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skill</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">

        <div v-for="skill in skills" :key="skill" class="pill">
           <span @click="deleteSkill(skill)">{{ skill }}</span> 
        </div>

        <div class="terme">
            <input type="checkbox" v-model="terms">
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create An Account</button>
        </div>
       
    </form>
    <p>email: {{ email }}</p>
    <p>passowrd: {{ password }}</p>
    <p>role: {{ role }}</p>
    <p>accept terms: {{ terms }}</p>
    

</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role:'designer',
            terms: false,
            tempSkill: '',
            skills:[],
            passwordError: ''
            
        }
    },
    methods: {
        addSkill(e){
            if (e.key == 'Alt' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill)){

                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
               
            }
           
        },
        deleteSkill(skill) {
            this.skills = this.skills.filter((item)=> {
                return skill !== item
            })

        },
        handleSubmit(){
            //validate password
            this.passwordError = this.password.length > 5 ? '' : 'Passowrd must be at least 6 chars long'
            if(!this.passwordError) {
                console.log('email:', this.email)
                console.log('password:', this.password)
                console.log('role:', this.role)
                console.log('skills:', this.skills)
                console.log('terms:', this.terms)

            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
    label {
        color: #aaa;
        display: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input, select {
        margin-top: 5px;
        margin-bottom: 10px;
        display: block;
        padding: 10px 6px;
        width: 100%;
        border-radius: 10px;
        box-sizing: border-box;
        border: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        position: relative;
        top: 2px;
    }
    .pill {
        display: inline-block;
       margin-left: 5px;
        padding: 6px 12px ;
        border-radius: 5px;
        background: #eee;
        font-size: 12px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }

    button {
        background:#0b6dff;
        border:0;
        padding: 10px 20px;
        color: white;
        border-radius: 20px;
    }
    .submit {
        text-align: center;
    }
    .error {
        color: #ff0062;
        font-size: 0.8em;
        font-weight: bold;
    }

</style>