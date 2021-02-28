<template>
  <div>
    <ValidationObserver ref="formValidator" v-slot="{ handleSubmit }">
      <form @submit.prevent="handleSubmit(submit)">
        <h2>New Person</h2>
        <div :class="$style.field">
          <label>First Name</label>
          <validation-provider
            vid="firstName"
            rules="required"
            v-slot="{ errors }"
          >
            <input v-model="fields.firstName" type="text" />
            <span :class="$style.error">{{ errors[0] }}</span>
          </validation-provider>
        </div>
        <div :class="$style.field">
          <label>Last Name</label>
          <validation-provider
            vid="lastName"
            rules="required"
            v-slot="{ errors }"
          >
            <input v-model="fields.lastName" type="text" />
            <span :class="$style.error">{{ errors[0] }}</span>
          </validation-provider>
        </div>
        <div :class="$style.field">
          <label>Email</label>
          <validation-provider vid="email" rules="required" v-slot="{ errors }">
            <input v-model="fields.email" type="text" />
            <span :class="$style.error">{{ errors[0] }}</span>
          </validation-provider>
        </div>
        <button>Submit</button>
      </form>
    </ValidationObserver>
  </div>
</template>

<script>
import { extend, ValidationObserver, ValidationProvider } from "vee-validate";
import { required } from "vee-validate/dist/rules";

extend("required", {
  ...required,
  message: "This field is required"
});

const blank = Object.freeze({
  firstName: "",
  lastName: "",
  email: ""
});

export default {
  components: {
    ValidationObserver,
    ValidationProvider
  },
  data: () => ({
    fields: { ...blank }
  }),
  methods: {
    submit() {
      this.$refs.formValidator.setErrors({
        email: "Duplicate email address"
      });
    }
  }
};
</script>

<style lang="scss" module>
form {
  display: flex;
  flex-direction: column;

  $button-text-color: #eee;
  $button-background-color: #888;

  > button {
    width: fit-content;
    padding: 0.5em;
    font-size: 1em;
    background-color: $button-background-color;
    border: solid 1px #555;
    color: $button-text-color;
    font-weight: bold;

    &:hover:not(:disabled) {
      cursor: pointer;
      color: lighten($button-text-color, 20%);
      background-color: lighten($button-background-color, 20%);
    }

    &:disabled {
      opacity: 0.7;
      cursor: not-allowed;
    }
  }

  h2 {
    color: #eee;
    margin: 0;
    margin-bottom: 0.5em;
  }

  width: 600px;
  border: solid 2px cyan;
  background-color: darkcyan;
  padding: 1em;

  .field {
    display: flex;
    align-items: center;

    > label {
      width: 6em;
      margin-right: 1em;
      font-size: 1.2em;
      font-weight: 700;
      color: #eee;
    }

    > span {
      display: flex;
      flex-direction: column;
      flex-grow: 1;

      > .error {
        margin-top: 0.5em;
        color: #f51720;
        font-weight: bold;
      }

      > input {
        width: 100%;
        font-size: 1em;
        padding: 0.5em;
        border-radius: 3px;
        border: solid 1px #bbb;
      }
    }

    &:not(:last-child) {
      margin-bottom: 0.5em;
    }
  }
}
</style>
