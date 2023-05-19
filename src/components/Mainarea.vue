<template>
  <section class="home-section">
    <div class="container px-sm-5 pl-xs-4">
      <div class="row">
        <div class="col-lg-4 col-md-6 col-sm-12 col1">
          <div class="section">
            <h3>Company Info</h3>
            <p>
              A company, abbreviated as co., is a legal entity representing an
              association of people, whether natural, legal or a mixture of
              both, with a specific objective.<br />
              Company members share a common purpose and unite to achieve
              specific, declared goals. <br />
              Company members share a common purpose and unite to achieve
              specific, declared goals.
            </p>
          </div>
        </div>
        <div class="col-lg-4 col-md-6 col-sm-12 col2">
          <div class="section">
            <h3>Instuctions</h3>
            <p>
              Read the questions carefully and confine your responses to an
              analysis of the questions as written. Do not assume any facts not
              set forth in the questions.
              <br />
              The average score for a set of examinations can be found by adding
              the scores of all the examinations and then dividing the total by
              the number of examinations.
            </p>
          </div>
        </div>
        <div class="col-lg-4 col-md-12 col-sm-12 form col3">
          <div class="section">
            <h3>Let's Start</h3>
            <form>
              <div class="mb-3">
                <label for="name" class="form-label">Name</label>
                <input v-model="nameInput" type="text" class="form-control" id="name" placeholder="Enter your name" />
              </div>
              <div class="mb-3">
                <label for="email" class="form-label">Email</label>
                <input v-model="emailInput" type="email" class="form-control" id="email" placeholder="Enter your email" />
              </div>
              <div class="mb-3">
                <label for="message" class="form-label">Message</label>
                <textarea v-model="messageInput" class="form-control" id="message" rows="4"
                  placeholder="Enter your message"></textarea>
              </div>
              <button @click="submited()" type="submit" class="btn">
                Submit
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

import axios from "axios";
export default {
  name: "Mainarea",
  data() {
    return {
      nameInput: "",
      emailInput: "",
      messageInput: "",
      changeTab: "",
      
    };
  },

  mounted() {
    document.addEventListener('visibilitychange', this.handleVisibilityChange);
  },
  beforeDestroy() {
    document.removeEventListener('visibilitychange', this.handleVisibilityChange);
  },

  methods: {
    submited() {
      axios.post('http://localhost:3000/result', {
        Name: this.nameInput,
        E_mail: this.emailInput,
        Message: this.messageInput
      })
      alert("Data is saved!");
  },

  async handleVisibilityChange() {
      if (document.visibilityState === 'hidden') {
        // Create a JSON object with the message data
        const messageData = {      
          changeTab: "Yes,Tab Changed" 
        };

        try {
          // Make an HTTP POST request to send the message data to the server
          const response = await axios.post('http://localhost:3000/result', messageData);
          
          // Handle the response from the server if needed
          console.log(response.data);
        } catch (error) {
          // Handle any errors that occur during the request
          console.error(error);
        }
      }
    }

},
};
</script>

<style scoped>
.home-section {
  /* position: relative; */
  /* left: 54px; */
  margin-top: 64px;
  padding: 10px 0px 64px 0px;
  background-color: #e4e9f7;
  min-height: 100vh;
  width: 100%;
  /* min-width: 50px; */
}

.row {
  /* margin-left: 55px; */
  padding-top: 20px;
}

@media only screen and (max-width: 767px) {
  .row {
    margin-left: 55px;
  }
}

.col1 h3,
.col2 h3,
.form .section h3 {
  text-align: center;
  background-color: #6b6e70;
  padding: 5px;
  color: #86c232;
}

.col1 p,
.col2 p {
  text-align: justify;
  background-color: #aaaeb1;
  padding: 10px;
  line-height: 1.5;
  font-size: 18px;
}

.section {
  background-color: #aaaeb1;
}

form {
  padding: 10px;
}

.btn {
  background-color: #86c232;
  color: #fff;
}
</style>
