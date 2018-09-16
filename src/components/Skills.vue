<template>
  <div class="hello">
   <!-- {{name}}
   <br/>
   {{btnState?'The button state is diasbled':'The button state is enabled'}}
   <button  v-on:click="changeName" v-bind:disabled="btnState">Change Name</button>  -->

    <div  class="holder">
      
       <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have ..." v-model="skill" v-validate="'min:5'"  name="skill"/>

      <transition  name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
      <p  class="alert"  v-if="errors.has('skill')" >{{errors.first('skill')}}</p>
      </transition>
      <!-- <input type="checkbox" id="checkbox" v-model="checked" /> -->
       </form>
      <!-- {{skill}} -->

      <ul>
        <!-- <li v-for='(data, index) in skills' :key='index'>{{ index}}. {{data.skill}} </li> -->
        <transition-group enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
        <li v-for='(data, index) in skills' :key='index'>{{data.skill}} </li>
        </transition-group>


      </ul>

      <p> These are  the  skills that you possess </p>

      <!-- <div v-bind:class="{alert: showAlert, 'anathorclass':true}"></div> -->

      <!-- class binding -->
      <!-- <div v-bind:class="alertObject"></div> -->
      <!-- style binding -->
      <!-- <div v-bind:style="{backgroundColor:bgColor,width:bgWidth,height:bgHeight}"></div> -->

      <!-- <p v-if="skills.length > 1 ">You have more than one skill</p>
      <p v-else>You have more than one or less skill</p> -->
    </div> 
  </div>
</template>

<script>
export default {
  name: "Skills",
  props: {},
  data() {
    return {
      name: "Niranjan",
      btnState: true,
      changeName: function() {},
      checked: false,
      skill: "",
      skills: [
        { skill: "vue.js" },
        { skill: "Node.js" },
        { skill: "Angular.js" }
      ],
      // alert: true,
      // anathorclass: true,
      alertObject: {
        alert: true,
        anathorclass: true
      },
      bgColor: "red",
      bgWidth: "200px",
      bgHeight: "500px"
    };
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.skills.push({ skill: this.skill });
          this.skill = "";
        } else {
          console.log("Not Valid Input");
        }
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css";

/* .alert {
  background-color: brown;
  width: 100%;
  height: 30px;
}
.anathorclass {
  border: 2mm;
  border-style: solid;
  border-color: black;
} */

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
  background-color: transparent;
  color: #687f7f;
}

.alert {
  background: yellowgreen;
  font-weight: bold;
  display: inline;
  padding: 5px;
}

.alert-in-enter-active {
  animation: bounce-in 0.5s;
}
.alert-in-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>
