<template>
    <div>
        <!--prevent the page from reloading after submitting-->
      <form @submit.prevent="handleSubmit">

        <label>Email:</label>
        <input type="email" required v-model="email">
  
        <label>Password:</label>
        <input type="password" required v-model="password">
        <div v-if="passwordError" class="error">{{ passwordError }}</div>
  
        <label>Role:</label>
        <select v-model="role">
          <option value="Web Developer">Web Developer</option>
          <option value="Android Developer">Android Developer</option>
        </select>
  
        <label>Type:</label>
        <div>
          <input type="checkbox" value="On-site" v-model="type">
          <label>On-site</label>
        </div>
        <div>
          <input type="checkbox" value="Remote" v-model="type">
          <label>Remote</label>
        </div>
        <div>
          <input type="checkbox" value="Hybrid" v-model="type">
          <label>Hybrid</label>
        </div>
  
        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">
        <div v-for="skill in skills" :key="skill" class="skills">
          <span @click="deleteSkill(skill)">{{ skill }}</span>
        </div>
  
        <div class="terms">
          <input type="checkbox" v-model="terms" required>
          <label>I have read and accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Submit</button>
        </div>

      </form>

      <p>Email: {{ email }}</p>
      <p>Password: {{ password }}</p>
      <p>Role: {{ role }}</p>
      <p>Terms accepted: {{ terms }}</p>
      <p>Type: {{ formattedType }}</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        email: "",
        password: "",
        role: "",
        terms: false,
        type: [],
        tempSkill: "",
        skills: [],
        passwordError: ""
      };
    },
    computed: {
      formattedType() {
        return this.type.join(', ');
      }
    },
    methods: {
        //add the skill to the input field when the user presses ","
      addSkill(e) {
        if (e.key === "," && this.tempSkill) {
          if (!this.skills.includes(this.tempSkill)) {
            this.skills.push(this.tempSkill);
          }
          this.tempSkill = "";
        }
      },
      deleteSkill (skill) {
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },
      handleSubmit () {
        //validate password
        this.passwordError = this.password.length > 5 ?
        alert("Form Submitted!") : "Password must be at least 6 characters long"

        if (!this.passwordError) {
            console.log("email: ", this.email);
            console.log("password: ", this.password);
            console.log("roles: ", this.roles);
            console.log("skills: ", this.skills);
            console.log("terms accepted: ", this.terms);
        }
      }
    }
  };
  </script>
  
  <style>
  form {
    max-width: 330px;
    margin: 30px auto;
    background-color: #2E3440;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
    border: 10px solid #AB9C41;
  }
  label {
    color: white;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input,
  select {
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
  .skills {
    display: inline-block;
    margin: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: rgb(0, 0, 0);
    cursor: pointer;
  }
  button {
    background: #AB9C41;
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
    color: #FF3131;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
  }
  </style>
  