<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
  <div>
    <!-- 1. Template Syntax -->
      <!-- 1a Text interpolation-->
    <p>This is task {{ message }} for SIT120</p>

    
     <!-- Input for First Name (Will be used in computed properties) -->
     <label for="first-name">First Name:</label>
    <input type="text" id="first-name" v-model="firstName" />

     <!-- Input for Last Name (Will be used in computed properties)-->
     <label for="last-name">Last Name:</label>
    <input type="text" id="last-name" v-model="lastName" />
    
    <!-- 1b. Raw HTML using v-html -->
    <div v-html="rawHtml"></div>
    
    <!-- 1c. Attribute Bindings -->
    <input :id="inputId" v-model="inputId"/>
    <p>{{ inputId }}</p>
    
    <!-- 1d. JavaScript expressions inside syntax -->
    <p>
      Is it weekend yet? {{ isWeekend(new Date()) ? 'Yes' : 'No' }}
    </p>

    <!-- 8. Form Input Bindings input type="text"-->
    <label for="name">Name:</label>
    <input type="text" id="name" v-model="name" />
    <!-- 1b. Raw HTML using v-html -->
    <span v-html="breakTag"></span>
    <span v-html="breakTag"></span>
    
    <!-- 8a. Form Input Bindings input type="radio"-->
    <label>Gender:</label>
    <input type="radio" id="male" value="Male" v-model="gender" />
    <label for="male">Male</label>
    <input type="radio" id="female" value="Female" v-model="gender" />
    <label for="female">Female</label>

    <span v-html="breakTag"></span>
    <span v-html="breakTag"></span>
    <!-- 8a. Form Input Bindings input type="checkbox"-->
    <div>
      <label>Subscribe to Newsletter:</label>
      <input type="checkbox" id="subscribe" v-model="subscribe" />
    </div>

    <span v-html="breakTag"></span>
   
     <!-- 8a. Form Input Bindings <select>-->
    <div>
      <label for="country">Country:</label>
      <select id="country" v-model="selectedCountry">
        <option value="Usa">USA</option>
        <option value="Canada">Canada</option>
        <option value="UK">UK</option>
        <option value="Australia">Australia</option>
      </select>
    </div>

    <span v-html="breakTag"></span>

      <!-- 8a. Form Input Bindings <textarea> -->
    <label for="textarea-input">Feedback:  </label>
    <textarea id="textarea-input" v-model="textAreaContent"></textarea>

    <span v-html="breakTag"></span>
    <span v-html="breakTag"></span>

     <!-- 8b. v-model modifiers -->
    
    <!-- Lazy Modifier -->
    <label for="lazy-input">Lazy Modifier:</label>
    <input type="text" id="lazy-input" v-model.lazy="lazyText" />
    <span v-html="breakTag"></span>
    <span> {{ lazyText }} </span>

    <span v-html="breakTag"></span>
    <span v-html="breakTag"></span>

    <!-- Number Modifier -->
    <label for="number-input">Number Modifier:</label>
    <input type="number" id="number-input" v-model.number="numericValue" />
    <span style="color: red;">  Please enter a valid numerical value.</span>

    <span v-html="breakTag"></span>
    <span v-html="breakTag"></span>

    <!-- Trim Modifier -->
    <label for="trim-input">Trim Modifier:</label>
    <input type="text" id="trim-input" v-model.trim="trimmedText" />
    <span v-html="breakTag"></span>
    <span> {{ trimmedText }}</span>

    <span v-html="breakTag"></span>
    <span v-html="breakTag"></span>

    <!-- 7. Event Handling: Listening to Events Method Handlers -->
    <button @click="submittedForm">Submit</button>
     <!-- 7. Event Handling: Listening to Events Inline Handlers -->
     <button @click="attandence++">Check Tickets</button>
    <p>Attendance: {{ attandence }}</p>
    <span v-if="attandence >= 5">Sold Out</span>
    <span v-else>Not Yet Sold Out</span>
    <!-- Display Form Data -->
    <div v-if="showFormData">
      <h2>Form Data:</h2>
      <p>Name: {{ name }}</p>
      <p>Gender: {{ gender }}</p>
      <p>Subscribed: {{ subscribe ? 'Yes' : 'No' }}</p>
      <p>Selected Country: {{ selectedCountry }}</p>
      <p>Feedback: {{ textAreaContent }}</p>
      <p>Number of people filled the form: {{ submissionCount }}</p>
      <p>Computed name: {{ fullName }}</p>
    </div>
     <!-- 10.Components props, events & slots -->
     <child-component 
       :message="messageFromParent" @childEvent="handleChildEvent">
      <p>This message came from child component!</p>
    </child-component>

    <!-- 5a. Binding HTML class -->
    <div :class="{ 'active': isActive, 'error': hasError }">5a Binding HTML Classes</div>

    <!-- 5b. Binding Inline Styles -->
    <div :style="dynamicStyles">5b Binding Inline Styles</div>
  
  </div>
</template>

<script>
// Reactivity Fundamentals ref()
import { ref, computed } from 'vue';
import childComponent from './childComponent.vue'; // Import the child component
export default {
  components: { childComponent },
  data() {
    return {
      message: '2.3C',
      rawHtml: '<p style="color: blue; font-size: 20px; <strong style="font-weight: bold;">This is a rawHTML, Vue.js</strong> example."  </p>',
      inputId: 'my-input',
      isTrue: true,
      name: '',
      gender: '',
      subscribe: false,
      selectedCountry: '',
      breakTag: '<br>',
      textAreaContent:"",
      lazyText: '',
      numericValue: null,
      trimmedText: '',
      attandence: 0,
      messageFromParent: 'Hello from Parent',
      isActive: true,
      hasError: false,
      dynamicStyles: {
        color: 'blue',
        fontSize: '20px',
      },

    };
  },
  //Reactivity Fundamentals <script setup>
  setup() {
    const submissionCount = ref(0);
    const showFormData = ref(false);
    const submittedForm = () => {
      submissionCount.value++;
      // Set the flag to true to display form data
      showFormData.value = true;
    };
    const firstName = ref('');
    const lastName = ref('');
    const fullName = computed(() => {
      return firstName.value + ' ' + lastName.value;})
    return{
      submittedForm,
      submissionCount,
      showFormData,
      firstName,
      lastName,
      fullName,
    };
  },
  //Watchers 
watch: {
  attandence(newAttendance, oldAttendance) {
    // Handle the change in attendance here
    console.log(`Attendance changed from ${oldAttendance} to ${newAttendance}`);
  }
},

  // 2. Methods
  methods: {
    // Function to check if a given date is a weekend
    isWeekend(date) {
      const day = date.getDay(); 
      return day === 0 || day === 6; 
    },
    handleChildEvent(data) {
      // Handle the event emitted by the child component here
      console.log('Received event from child component:', data);
  },
},
};
</script>





<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
