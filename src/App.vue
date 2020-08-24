<template>
  <form 
    class="form_cnt"
  >
    <div v-if="errors.length">
      <ul class="form_detail">
        <li 
          v-for="error in errors" 
          :key="error.index"
        >
          <i class="fas fa-exclamation-triangle" />
          {{ error }}
        </li>
      </ul>
    </div>
    <div class="notification">
      <!-- USER NAME -->
      <div class="field form-group">
        <label class="label">
          نام کاربری
        </label>
        <div class="control">
          <input 
            v-model="userName"
            class="input" 
            type="text" 
            placeholder="نام کاربری" 
            @change="checkUserInput"
          >
        </div>
      </div>
      <!-- NATIONAL CODE -->
      <div class="field">
        <label class="label">
          کد ملی
        </label>
        <div class="control has-icons-left has-icons-right">
          <input 
            v-model="nationalCode"
            class="input" 
            type="text" 
            placeholder="کد ملی"
            @change="checkCodeInput"
          >
          <span class="icon is-small is-left">
            <i class="fas fa-user" />
          </span>
          <span class="icon is-small is-right">
            <i class="fas fa-check" />
          </span>
        </div>
      </div>
      <!-- PHONE -->
      <div class="field">
        <label class="label">
          موبایل
        </label>
        <div class="control has-icons-left has-icons-right">
          <input 
            id="phone" 
            v-model="phone"
            class="input" 
            type="tel" 
            placeholder="موبایل" 
            @change="checkPhoneInput"
          >
          <span class="icon is-small is-left">
            <i class="fas fa-phone" />
          </span>
          <span class="icon is-small is-right">
            <i class="fas fa-check" />
          </span>
        </div>
      </div>
      <!-- PASSWORD -->
      <div class="field">
        <label class="label">
          رمز عبور
        </label>
        <div class="control has-icons-left has-icons-right">
          <input
            id="password" 
            v-model="password"
            class="input" 
            type="password" 
            placeholder="رمز عبور" 
            @change="checkPassInput"
          >
          <span class="icon is-small is-left">
            <i class="fas fa-lock" />
          </span>
          <span class="icon is-small is-right">
            <i class="fas fa-check" />
          </span>
        </div>
      </div>
      <!-- CONFIRM PASSWORD -->
      <div class="field">
        <label class="label">
          تکرار رمز عبور
        </label>
        <div class="control has-icons-left has-icons-right">
          <input 
            id="confirm_pass"
            v-model="confirmPass" 
            class="input" 
            type="password" 
            placeholder="تکرار رمز عبور" 
            @change="checkConfInput"
          >
          <span class="icon is-small is-left">
            <i class="fas fa-lock" />
          </span>
          <span class="icon is-small is-right">
            <i class="fas fa-check" />
          </span>
        </div>
      </div>
      <div class="field is-grouped">
        <div>
          <button 
            class="button is-link"
            @click="checkForm"
          >
            ثبت نام
          </button>
        </div>
        <div class="control">
          <button 
            class="button is-link is-light"
            @click="clearData"
          >
            لغو
          </button>
        </div>
      </div>
    </div>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        errors: [],
        name: null,
        confirmPass: null,
        pwd : null,
        phone : null,
        nationalCode: null,
      }
    },
    methods: {
      checkForm: function (e) {
        this.errors = [];

        //---------- USER NAME ----------//
        if (!this.userName) {
          this.errors.push("پر کردن نام کاربری الزامی است");
        } else if (!this.validUser(this.userName)) {
          this.errors.push('نام کاربری معتبر نیست');
        }

        //---------- NATIONAL CODE ----------//
        if (!this.nationalCode) {
          this.errors.push('پر کردن کد ملی الزامی است');
        } else if (!this.validNationalCode(this.nationalCode)) {
          this.errors.push('کد ملی معتبر نیست');
        }

         //---------- PHONE ----------//
        if (!this.phone) {
          this.errors.push('پر کردن شماره تلفن همراه الزامی است');
        } else if (!this.validPhone(this.phone)) {
          this.errors.push('تلفن همراه معتبر نیست');
        }

        //---------- PASSWORD ----------//
        if (!this.password) {
          this.errors.push('رمز عبور را انتخاب نمایید');
        } else if (!this.validPassword(this.password)) {
          this.errors.push(' رمز عبور معتبر نیست');
        }

        //---------- CONFIRM PASSWORD ----------//
        if (!this.confirmPass) {
          this.errors.push('رمز عبور خود را مجددا وارد نمایید');
        } else  if (!this.validConfirmPass(this.confirmPass)) {
          this.errors.push('رمز عبور مجدد معتبر نیست');
        }

        if (!this.errors.length) {
          alert ('ثبت نام با موفقیت انجام شد');
        }

        e.preventDefault();
      },

      checkUserInput: function(){
        let input = event.target
        if (!this.validUser(this.userName)) {
          input.classList.add("main_red");
        } else {
          input.classList.remove("main_red");
        }
      },

      checkCodeInput: function(){
        let input = event.target
        if (!this.validNationalCode(this.nationalCode)) {
          input.classList.add("main_red");
        } else {
          input.classList.remove("main_red");
        }
      },

      checkPhoneInput: function(){
        let input = event.target
        if (!this.validPhone(this.phone)) {
          input.classList.add("main_red");
        } else {
          input.classList.remove("main_red");
        }
      },

      checkPassInput: function(){
        let input = event.target
        if (!this.validPassword(this.password)) {
          input.classList.add("main_red");
        } else {
          input.classList.remove("main_red");
        }
      },

      checkConfInput: function(){
        let input = event.target
        if (!this.validConfirmPass(this.confirmPass)) {
          input.classList.add("main_red");
        } else {
          input.classList.remove("main_red");
        }
      },

      clearData: function() {
        this.userName = null;
        this.confirmPass = null;
        this.password = null;
        this.phone = null;
        this.nationalCode = null;
      },

      validUser : function (userName) {
        let testUser = /^(?=.{3,20}$)(?![_.])(?![0-9])[a-zA-Z0-9._]+(?<![_.])$/;
        return testUser.test(userName);
      },

      validPhone : function (phone) {
        let testPhone =  /^\(?([0]{1})\)?([9]{1})?([0-9]{9})$/;
        return testPhone.test(phone);
      },

      validPassword : function (password) {
        let testPass =  /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,20}$/;
        return testPass.test(password);
      },

      validConfirmPass : function () {
        return (this.password == this.confirmPass);
      },

      validNationalCode : function (nationalCode) {
        if (/^\d{10}$/.test(nationalCode)) {
          let check = parseInt(nationalCode[9]);
          let sum = 0;
          let i;
          for (i = 0; i < 9; ++i) {
            sum += parseInt(nationalCode[i]) * (10 - i);
          }
          sum %= 11;
          if ((sum < 2 && check == sum) || (sum >= 2 && check + sum == 11)) {
            return true;
          } else {
            return false;
          }
        }
      }
    }
  }
</script>