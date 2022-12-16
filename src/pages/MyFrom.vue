
<template>
  <q-page class="column items-center justify-center">
    <q-card class="create-account-card">
      <q-form>
        <q-card-section>
          <div class="text-h6">Create New Account</div>
          <div class="text-subtitle1">
            Fill out the following form to create your new account.
          </div>
        </q-card-section>
        <q-separator inset />
        <q-card-section class="column q-gutter-md">
          <q-input label="Name *" v-model="FormState.name"></q-input>
          <q-input label="Email *" v-model="FormState.email"></q-input>
          <q-input label="Phone" v-model="FormState.phone" mask="(###) ### - ####" fill-mask
            hint="(###) ### - ####"></q-input>
          <q-input label="Password *" type="password" v-model="FormState.password.value"></q-input>
          <div class="password-criteria q-pa-sm">
            <div class="text-subtitle2 q-mb-sm">Password Criteria:</div>
            <div>
              <q-icon name="cancel" color="negative"></q-icon>
              Must be at least 12 characters long.
            </div>
            <div>
              <q-icon name="cancel" color="negative"></q-icon>
              Must contain at least one capital letter.
            </div>
            <div>
              <q-icon name="cancel" color="negative"></q-icon>
              Must contain at least one number.
            </div>
            <div>
              <q-icon name="cancel" color="negative"></q-icon>
              Must contain at least one symbol.
            </div>
          </div>
          <q-input label="Confirm Password *" type="password" v-model="FormState.password.confirm"></q-input>
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
      }
    }
  },
  methods: {

  },
  mounted () {

  }
}
</script>
