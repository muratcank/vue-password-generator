<script>
export default {
  name: 'App',

  components: {},

  data: () => ({
    password: null,
    passwordLength: 8,
  }),

  methods: {
    getRandomInt(max) {
      return Math.floor(Math.random() * Math.floor(max));
    },
    generatePassword() {
      const lowerCaseLetters = 'abcdefghijklmnopqrstuvwxyz'.split('');
      const upperCaseLetters = 'abcdefghijklmnopqrstuvwxyz'.toUpperCase().split('');
      const numbers = '1234567890'.split('');
      const specialCharacters = '*/\\(){}[],.!?=\'"'.split('');

      const pool = lowerCaseLetters
        .concat(upperCaseLetters)
        .concat(numbers)
        .concat(specialCharacters);

      const tempPassword = [];

      for (let index = 0; index < this.passwordLength; index += 1) {
        const randomIndex = this.getRandomInt(pool.length);
        tempPassword.push(pool[randomIndex]);
      }

      this.password = tempPassword.join('');
    },
    copyPassword() {
      if (this.password === '') return false;

      return navigator.clipboard.writeText(this.password);
    },
  },
};
</script>

<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <span>Vue Password Generator</span>
    </v-app-bar>

    <v-main>
      <v-container fill-height>
        <v-row justify="center">
          <v-col class="text-center">
            <v-text-field
              v-model="passwordLength"
              name="passwordLength"
              label="Password Length"
            />
          </v-col>

          <v-col class="text-center">
            <v-btn
              color="success"
              outlined
              elevation="0"
              @click="generatePassword"
            >
            Generate Password
          </v-btn>
          </v-col>

          <v-col class="text-center">
            <v-text-field
              v-model="password"
              name="password"
              label="Password"
            />

            <v-btn color="success" @click="copyPassword" depressed>
              Copy
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>
