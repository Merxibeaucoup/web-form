<template>

<!---Vue form using v-model 2 way data binding--->
  <form @submit.prevent="handleSubmit">
    <label> Email: </label>
    <input type="email" required v-model="email">

    <label> Password: </label>
    <input type="password" required v-model="password">
    <!--- if password is true, display password error-->
    <div v-if="passwordError" class="error"> {{ passwordError }}</div>

     <label> Role: </label>
    <select v-model="role"> 
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
    </select>

    <label >skills: </label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" >
        <!--- skill passed in a s an argument ...at click the skill will delete -->
            <span @click="deleteSkill(skill)"> {{skill}}</span>
    </div>


    <div class="terms">
        <input type="checkbox" required v-model="terms">
        <label > Accept terms and conditions</label>
    </div>


    <div class="submit">
        <button> Create</button>
    </div>



  </form>

  <p> Email: {{email}}</p>
   <p> password: {{password}}</p>
    <p> role: {{role}}</p>
    <p> terms: {{terms}}</p>
    <p> skills: {{tempSkill}}</p>
     

</template>

<script>
export default {
    data(){
        return{
            // anything typed or selcted in the form fields is also updated and tracked in this data field as well
            email: '',
            password: '',
            role: '',
            //terms initialized to false , when toggled(checked) its gonna set to true 
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError:''
           

        }
    }, methods:{
        
        addSkill(e){
            // if user enters an input followed by a comma , the event fires 
            // adds it to the skills array
            //then clears and resets the field 
            if (e.key === "," && this.tempSkill){
                // checks to see if the skills array already includes the new input(tempSkill)
                // if it doesnt include it , its gonna be true 
                // and then the new input (tempSkill) will be added 
                if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill)

                }
                this.tempSkill = ''

            }

        },

        // on click deletes the skill 
        deleteSkill(skill){
            
            // filter method ccycles through array and finds a fucntion for each item
            // if true , item is kept in the array
            // if false , item is removed from the array 

            // checks if the skill is equal to the item
            // if it does, returns false and item is removed
            this.skills = this.skills.filter((item) =>{
                // if not equal , returns true and items stays in the array 
                return skill !== item

            })
        },
        handleSubmit(){
            //VALIDATE password
            // if password is =< 5 , throws an error
            this.passwordError = this.password.length > 5 ? 
            '' : 'password must be atleast 6 characters long'

            //if no error 
            if(!this.passwordError){
                console.log('email: ', this.email)
                console.log('password: ', this.password)
                console.log('role: ', this.email)
                console.log('skills: ', this.skills)
                console.log('terms accepted: ', this.terms)
                
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

input[type ="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: -4px;
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
    color:#777;
    cursor: pointer;
}

button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
}
.submit{
    text-align: center;
}

.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>