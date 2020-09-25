<template>
  <div>
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input
          type="text"
          placeholder="Enter a skill you have..."
          v-model="skill"
          name="skill"
        />
        <p class="alert" v-if="skillMoreThanFive">
          {{ error }}
        </p>
      </form>
      <ul>
        <li v-for="(skill, index) in skills" :key="index">{{ skill.skill }}</li>
      </ul>
      <p>These are the skills that you possess</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Skills",
  data() {
    return {
      skill: "",
      error: "Min length of skill must be 5 characters",
      skills: [
        { skill: "vue.js" },
        { skill: "Frontend developer" },
        { skill: "react" },
      ],
      showAlert: true,
      alertObject: {
        alert: true,
      },
    };
  },
  computed: {
    skillMoreThanFive() {
      return this.skill.length >= 1 && this.skill.length < 5;
    },
  },
  methods: {
    addSkill() {
      if (this.skill.length >= 5) {
        this.skills.push({ skill: this.skill });
        this.skill = "";
        this.error = "";
      } else {
        this.error = "Min length of skill must be 5 characters";
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.holder {
  background: #fff;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}

p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}

.container {
  box-shadow: 0px 0px 40px lightgray;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}
</style>
