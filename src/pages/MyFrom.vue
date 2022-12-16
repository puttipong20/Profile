<template>
  <q-page class="column items-center justify-center">
    <q-card class="create-account-card">
      <q-form autofocus @submit="submitForm">
        <q-card-section>
          <div class="text-h6">Create New Account</div>
          <div class="text-subtitle1">
            Fill out the following form to create your new account.
          </div>
        </q-card-section>
        <q-separator inset />
        <q-card-section class="column q-gutter-md">
          <q-input label="Name *" v-model="FormState.name" :rules="[
            (val) => (val && val.length > 0) || 'Name must be filled in.',
          ]"></q-input>
          <q-input label="Email *" v-model="FormState.email"
            :rules="[(val) => validateEmail(val) || 'Must be a valid email.']"></q-input>
          <q-input label="Phone" v-model="FormState.phone" mask="(###) ### - ####" hint="(###) ### - ####"></q-input>
          <q-input label="Password *" v-model="FormState.password.value" type="password" :rules="[
            (val) =>
              validatePassword(val) || 'Password must meet all criteria.',
          ]">
          </q-input>
          <div class="password-criteria q-pa-sm">
            <div class="text-subtitle2 q-mb-sm">Password Criteria:</div>
            <div>
              <q-icon :name="ValidPassword.length ? 'check_circle' : 'cancel'"
                :color="ValidPassword.length ? 'positive' : 'negative'"></q-icon>
              Must be at least 12 characters long.
            </div>
            <div>
              <q-icon :name="ValidPassword.capital ? 'check_circle' : 'cancel'"
                :color="ValidPassword.capital ? 'positive' : 'negative'"></q-icon>
              Must contain at least one capital letter.
            </div>
            <div>
              <q-icon :name="ValidPassword.number ? 'check_circle' : 'cancel'"
                :color="ValidPassword.number ? 'positive' : 'negative'"></q-icon>
              Must contain at least one number.
            </div>
            <div>
              <q-icon :name="ValidPassword.symbol ? 'check_circle' : 'cancel'"
                :color="ValidPassword.symbol ? 'positive' : 'negative'"></q-icon>
              Must contain at least one special character: !@#$%^&*()-_+=
            </div>
          </div>
          <q-input label="Confirm Password *" v-model="FormState.password.confirm"
            :disable="!validatePassword(FormState.password.value)" type="password" :rules="[
              (val) =>
                (val && val === FormState.password.value) ||
                'Must match password.',
            ]">
          </q-input>
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat>Cancel</q-btn>
          <q-btn color="primary" type="submit">Create Account</q-btn>
        </q-card-actions>
      </q-form>
    </q-card>
  </q-page>
</template>

<style lang="scss">
.create-account-card {
  width: 512px;
}

.password-criteria {
  background-color: #efefef;
  border-radius: 0.5rem;
}
</style>

<script>
export default {
  name: 'MyFrom',
  components: {},
  data () {
    return {
      FormState: {
        name: '',
        email: '',
        phone: '',

        password: {
          value: '',
          confirm: ''
        }
      },
      ValidPassword: {
        length: false,
        capital: false,
        number: false,
        symbol: false
      }
    }
  },
  methods: {
    validateEmail (email) {
      return /[a-z0-9]+@[a-z]+\.[a-z]{2,3}/.test(email)
    },
    validatePassword (password) {
      // Test length
      this.ValidPassword.length = this.FormState.password.value.length >= 12

      // Test capital
      this.ValidPassword.capital = /^(?=.*[A-Z]).*$/.test(password)

      // Test number
      this.ValidPassword.number = /^(?=.*[0-9]).*$/.test(password)

      // Test symbol
      this.ValidPassword.symbol = /^(?=.*[!@#$%^&*-_+=]).*$/.test(password)

      return (
        this.ValidPassword.length &&
        this.ValidPassword.capital &&
        this.ValidPassword.number &&
        this.ValidPassword.symbol
      )
    }
  },
  mounted () {

  }
}
</script>
