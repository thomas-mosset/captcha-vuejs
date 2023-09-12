<template>
  <div class="main">
    <h1 class="title">Captcha in Vuejs</h1>

    <div class="captcha">
       <div
          v-for="(char, i) in captcha"
          :key="i"
          class="captcha-character"
          :style="{
            fontSize: getFontSize() + 'rem',
            fontWeight: getFontWeight(),
            transform: 'rotate(' + getRotationAngle() + 'deg)',
          }"
        >
          {{ char }}
        </div>
    </div>

    <button class="btn" @click="createCaptcha">Generate new captcha</button>

    <div class="user-response">
      <form @submit.prevent="submitCaptcha()">
        <label for="captcha" class="user-captcha-label">Enter captcha :</label>
        <input type="text" name="captcha" id="captcha" class="user-captcha-input" v-model="userCaptchaSubmission">

        <button type="submit" class="btn">Submit</button>
      </form>

      <p v-if="message !== ''">{{ message }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheCaptcha',
  data () {
    return {
      captchaLength: 8,
      captcha: [],
      userCaptchaSubmission: "",
      message: "",
    }
  },
  created() {
    this.createCaptcha();
  },
  methods: {
    createCaptcha() {
      let temporaryCaptcha = "";
      this.message = "";

      for (let i = 0; i < this.captchaLength; i++) {
        temporaryCaptcha += this.getRandomCharacter();
      }

      this.captcha = temporaryCaptcha.split("");
    },
    getRandomCharacter() {
      const characters = "abcdefghijklmnopqrstuvwxyz0123456789@!*";

      const randomNumber = Math.floor(Math.random() * 39); // 39 is the nb for possible characters
      
      return characters[randomNumber];
    },
    getFontSize() {
      const fontSizeVariations = [1, 1.5, 2, 3];

      return fontSizeVariations[Math.floor(Math.random() * 4)];
    },
    getFontWeight() {
      const fontWeightVariations = [400, 500, 700];

      return fontWeightVariations[Math.floor(Math.random() * 3)];
    },
    getRotationAngle() {
      const rotationVariations = [5, 10, 20, 25, -5, -10, -20, -25];

      return rotationVariations[Math.floor(Math.random() * 8)];
    },

    submitCaptcha() {
      this.message = "";

      const temporaryCaptchaToCompare = this.captcha.join(""); // transform array back to string

      if (this.userCaptchaSubmission.length === 0) {
        this.message = "You submitted an empty captcha. Please try again.";
      } else if (this.userCaptchaSubmission.length < this.captchaLength || this.userCaptchaSubmission.length > this.captchaLength) {
        this.message = "Entered captcha must be " + this.captchaLength + " long.";
      } else if (this.userCaptchaSubmission !== temporaryCaptchaToCompare) {
        this.message = "Please enter a valid captcha.";
      } else {
        this.message = "Captcha is valid !";
      }

      this.userCaptchaSubmission = "";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.captcha {
  margin: 5rem auto 2rem;
  border: solid #FCC9B5 2px;
  background: #FCC9B5;
  width: 20rem;
  height: 5rem;
  display: flex;
  justify-content: space-around;
  align-items: center;
  align-content: center;
}

.captcha-character {
  width: fit-content;
}

.btn {
  padding: 10px;
  background: #FCC9B5;
  border: 2px solid #000000;
  font-size: 16px;
  font-weight: bold;
}

.btn:hover {
  background: #fddacc;
  cursor: pointer;
}

.user-response {
  margin: 5rem auto;
}

.user-captcha-label,.user-captcha-input {
  margin-right: 0.5rem;
}

</style>
