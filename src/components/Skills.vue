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
        <transition
          name="alert-in"
          enter-active-class="animated flipInX"
          leave-active-class="animated flipOutX"
        >
          <p class="alert" v-if="skillMoreThanFive">
            {{ error }}
          </p>
        </transition>
      </form>
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp">
          <li v-for="(skill, index) in skills" :key="index + 0">
            {{ skill.skill }}
            <i class="fa fa-minus-circle" @click="removeSkill(index)"></i>
          </li>
        </transition-group>
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
      }
    },
    removeSkill(index) {
      this.skills.splice(index, 1);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
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
.alert {
  background: #fdf2ce;

  font-weight: bold;
  text-align: center;

  width: fit-content;

  padding: 5px;
  margin: 20px auto;
}

.alert-in-enter-active {
  animation: bounce-in 0.75s;
}

.alert-in-leave-active {
  animation: bounce-in 0.75s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

i {
  float: right;
  cursor: pointer;
}
</style>
