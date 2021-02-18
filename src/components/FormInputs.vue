<template>
  <div class="container">
    <div class="section_form">
      <h1>About</h1>
      <p>
        This is the TodoList app v1.0.0. It is part of the Vue crash course on
        Youtube
      </p>
      <form @submit.prevent="addTodo">
        <div class="form_input">
          <label>Name</label>
          <input type="text" required v-model="name" />
        </div>
        <div class="form_input">
          <label>Email:</label>
          <input type="email" v-model="email" />
        </div>
        <div class="form_input">
          <label>Password:</label>
          <input type="password" v-model="password" />
        </div>
        <div class="form_input">
          <label>Role:</label>
          <select v-model="role">
            <option value="developer">Developer</option>
            <option value="designer">Designer</option>
          </select>
        </div>
        <div class="form_input">
          <input type="checkbox" v-model="terms" />
          <label>accept terms and condition</label>
        </div>
        <div class="form_input">
          <label>Skills:</label>
          <input type="text" v-model="tempSkill" @keyup="addSkill" />
        </div>
        <div v-for="skill in skills" :key="skill">
          <div @click="deleteSkill(skill)">{{ skill }}</div>
        </div>
        <div class="form_input">
          <input type="submit" class="btn" name="Submitt" />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "FormInputs",
  components: {},
  data() {
    return {
      name: "",
      email: "",
      password: "",
      role: "developer",
      tempSkill: "",
      skills: [],
      terms: false,
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    addTodo() {
      console.log(this.name);
      const data = {
        // mock api data
        title: "foo",
        body: "bar",
        userId: 1,
      };

      axios
        .post("https://jsonplaceholder.typicode.com/posts", data)
        .then((res) => console.log(res))
        .catch((err) => console.log(err));
    },
  },
};
</script>


<style scoped>
.container {
  display: flex;
  justify-content: center;
}
.section_form {
  text-align: center;
}
form {
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
  font-size: 1em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input[type="text"],
input[type="password"],
input[type="email"],
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  font-size: 16px;
  border: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 20px;
  height: 20px;
  margin: 0 5px 0 0;
  position: relative;
  top: 2px;
}
.btn {
  display: block;
  padding: 10px 6px;
  width: 100%;
  margin-top: 50px;
}
</style>
