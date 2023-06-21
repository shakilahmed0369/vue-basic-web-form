<template lang="">
  <form @submit.prevent="handleForm">
    <label for="">Email:</label>
    <input v-model="email" type="email" required>

    <label for="">Password:</label>
    <input v-model="password" type="password" required>
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    <label for="">Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label for="">Skills:</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill">

    <div class="pill" v-for="skill in skills" :key="skill" @click="removeSkill(skill)">{{ skill }}</div>

    <div class="terms">
      <input v-model="terms" type="checkbox"  required>
      <label for="">terms and conditions</label>
    </div>
    <div class="submit">
      <button>Create Account</button>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      names: [],
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === ',' && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
          this.tempSkill = '';
        }
      }
    },
    removeSkill(skill) {
      let index = this.skills.indexOf(skill);
      this.skills.splice(index, 1);
    },
    handleForm() {
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at last 6 chars long'

      if(!this.passwordError) {
        console.log('email: ',  this.email);
        console.log('password: ',  this.password);
        console.log('role: ',  this.role);
        console.log('skills: ',  this.skills);
        console.log('terms accepted: ',  this.terms);

      }
    }
  },
}
</script>
<style lang="css">
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
  border-bottom: 1px solid #dddd;
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