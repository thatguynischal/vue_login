<template>
  <form @submit.prevent="handleSubmit">
    <label >Email: </label>
    <input type="email" required v-model="email">

    <label >Password: </label>
    <input type="password" required v-model="password">
    <div class="error" v-if="passwordError"> {{passwordError}}</div>

    <label>Role: </label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label>Skills: </label>
    <input type="text" v-model="tempSkills" @keyup.alt="addSkill">
    <div class="pill" v-for="skill in skills" :key="skill">
    <span @click="deleteSkill(skill)">
        {{ skill }}

    </span>
    </div>

    <div class="terms">
        <input type="checkbox" v-model="terms" required/>
        <label>Accept terms and conditions.</label>
    </div>

    <div class="submit">
        <button>Sign Up Boy</button>
    </div>

  </form>

</template>

<script>
export default {
    data(){
        return{
            email: "",
            password: "",
            role: "designer",
            terms: false,
            tempSkills: '',
            skills: [],
            passwordError: ""
        }
    },
    methods: {
        addSkill(e){
            if (e.key === ',' && this.tempSkills){
                if (!this.skills.includes(this.tempSkills)){
                    this.skills.push(this.tempSkills)
                }
                this.tempSkills = ""
            }
        },
        deleteSkill(skill){
         this.skills = this.skills.filter((item) => {
            return skill !== item
         })   
        },
        handleSubmit(){
            console.log("form submitted.")
            this.passwordError = this.password.length > 5 ? "" : "Password too freaking short."
            if (!this.passwordError){
                console.log(this.email)
                console.log(this.password)
                console.log(this.role)
                console.log(this.skills)
                console.log(this.terms)

            }
        }
        }

}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
    
}
input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}
.pill{
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
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
.error{
    color: red;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: bold;
}

</style>