<template>
  <v-container>
    <form>
    <v-text-field
      v-model="userData.name"
      :counter="10"
      label="نام"
      required
      @keyup.enter="checkUser"
      :rules="nameErrors"
    ></v-text-field>
    <v-text-field
      v-model="userData.lastName"
      :counter="15"
      label="نام خانوادگی"
      @keyup.enter="checkLastName"
      required
    ></v-text-field>
    <v-text-field
      v-model="userData.nationalCode"
      label="کدملی"
      :counter="10"
      :rules="errosBag"
      required
      @keyup.enter="checkNationalCode(nationalCode)"
    ></v-text-field>

    <v-btn
      class="mr-4"
      @click="submit"
    >
      ثبت نام
    </v-btn>
    <v-btn @click="clear">
      پاک کردن
    </v-btn>
  </form>
  </v-container>
</template>

<script>
  export default {
    name: 'Signup',

    data: () => ({
      userData: {
        name: '',
        lastName: '',
        nationalCode: '',
      },
      nameErrors: [
        value => {
          const patternName = /^(?=.{3,10}$)(?![_.])(?![0-9])[a-zA-Z0-9._]+(?<![_.])$/;
          return patternName.test(value) || 'نام کاربری نامعتبر است.'
        },
      ],
    }),
    methods: {
      checkName() {
      const patternName = /^(?=.{3,10}$)(?![_.])(?![0-9])[a-zA-Z0-9._]+(?<![_.])$/;
      if (this.userData.name.length === 0) {
        this.userData.name.nameErrors.push('وارد کردن نام الزامیست');
        return false;
      }
      if (patternName.test(this.name)) {
        return true;
      }

      this.userData.name.nameErrors.push('نام کاربری نامعتبر است');
      return false;
    },
      checkLastName() {
      const patternLastName = /^(?=.{3,15}$)(?![_.])(?![0-9])[a-zA-Z0-9._]+(?<![_.])$/;
      if (this.name.length === 0) {
        this.errorsBag.push('وارد کردن نام خانوادگی الزامیست');
        return false;
      }
      if (patternLastName.test(this.name)) {
        return true;
      }

      this.errorsBag.push('نام خانوادگی نامعتبر است');
      return false;
    },
    checkNationalCode() {
      let validCode = false;
      let sum = 0;

      if (this.nationalCode.length === 0) {
        this.errorsBag.push('لطفا کد ملی را وارد کنید');
        return false;
      }

      for (let i = 0; i < 9; i += 1) {
        sum += (this.nationalCode[i] * (this.nationalCode.length - i));
      }
      if (((sum % 11) >= 2 && (11 - (sum % 11)) === parseInt(this.nationalCode[9], 10))
      || ((sum % 11) < 2
        && (sum % 11) === parseInt(this.nationalCode[9], 10))) {
        validCode = true;
        return true;
      }
      if (!validCode) {
        this.errorsBag.push('کد ملی اشتباه وارد شده است.');
        return false;
      }
      return false;
    },
    clear() {
      this.userData.name = '',
      this.userData.lastName = '',
      this.userData.nationalCode = ''
    },
      submit() {
        this.errorsBag =[];
        if (this.checkName()
          && this.checkLastName()
          && this.checkNationalCode()
        )
        {
          alert ('yay');
        }
      }
    }
  }
</script>
<style>
  
</style>
