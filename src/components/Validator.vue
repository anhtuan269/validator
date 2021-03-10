<template>
  <div class="main">
    <form
      action=""
      method="POST"
      class="form"
      id="form-1"
      @submit.prevent="submit()"
    >
      <h3 class="heading">Thành viên đăng ký</h3>
      <p class="desc">Cùng nhau học lập trình miễn phí tại F8 ❤️</p>

      <div class="spacer"></div>

      <div class="form-group" :class="{ invalid: selectived }">
        <label for="fullname" class="form-label">Tên đầy đủ</label>
        <input
          id="fullname"
          name="fullname"
          type="text"
          placeholder="VD: Sơn Đặng"
          class="form-control"
          @blur="isRequired()"
          @input="nameForcus()"
        />
        <span class="form-message">{{ nameMessage }}</span>
      </div>

      <div class="form-group" :class="{ invalid: emailForm }">
        <label for="email" class="form-label">Email</label>
        <input
          id="email"
          name="email address"
          type="text"
          placeholder="VD: email@domain.com"
          class="form-control"
          @input="emailForcus()"
        />
        <span class="form-message">{{ emailMessage }}</span>
      </div>

      <div class="form-group" :class="{ invalid: phoneForm }">
        <label for="phone_number" class="form-label">Số điện thoại</label>
        <div class="phone-area">
          <input
            type="text"
            value="+84"
            style="text-align: center; border-radius: 2px"
            class="form-control"
          />
          <input
            id="phone_number"
            name="phone_number"
            type="text"
            placeholder=""
            class="form-control"
            @blur="isPhone()"
            @input="handlePhoneInput"
            :value="formattedPhoneNumber"
            maxlength="11"
          />
        </div>
        <span class="form-message">{{ phoneMessage }}</span>
      </div>

      <div class="form-group" :class="{ invalid: passwordForm }">
        <label for="password" class="form-label">Mật khẩu</label>
        <input
          id="password"
          name="password"
          type="password"
          placeholder="Nhập mật khẩu"
          class="form-control"
          @blur="isPass()"
          @input="passwordForcus()"
        />
        <span class="form-message">{{ passwordMessage }}</span>
      </div>

      <div class="form-group" :class="{ invalid: confirmForm }">
        <label for="password_confirmation" class="form-label"
          >Nhập lại mật khẩu</label
        >
        <input
          id="password_confirmation"
          name="password_confirmation"
          placeholder="Nhập lại mật khẩu"
          type="password"
          class="form-control"
          @blur="isConfirm()"
          @input="confirmForcus()"
        />
        <span class="form-message">{{ confirmMessage }}</span>
      </div>

      <button class="form-submit">Đăng ký</button>
    </form>
  </div>
</template>

<script >
export default {
  props: {},
  // mounted :function() {
  //     this.$nextTick( formatPhone

  //     )
  // },
  data() {
    return {
      selectived: false,
      emailForm: false,
      passwordForm: false,
      confirmForm: false,
      phoneForm: false,
      phoneMessage: "",
      confirmMessage: "",
      nameMessage: "",
      emailMessage: "",
      passwordMessage: "",
      regex: /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/,
      phone_regex: /([0-9]{3})+[-]+([0-9]{3})+[-]+([0-9]{3})\b/g,
      formattedPhoneNumber: "",
    };
  },
  computed: {},
  methods: {
    submit: function () {
      this.isRequired();
      //   this.isEmail();
      this.isPass();
      this.isConfirm();
      this.getData();
      this.isPhone();
      return;
    },
    isPhone: function () {
      if (
        this.phone_regex.test(document.querySelector("#phone_number").value) ===
        true
      ) {
        this.phoneForm = false;
        this.phoneMessage = "";
        console.log(document.querySelector("#phone_number").value);
      } else {
        this.phoneForm = true;
        this.phoneMessage = "số điện thoại không đúng định dang";
      }
      console.log(
        this.phone_regex.test(document.querySelector("#phone_number").value)
      );
      console.log(this.phoneForm);
    },
    getData: function () {
      var data = document.querySelectorAll("#form-1 input[name]");
      var formdata = Array.from(data).reduce(function (values, input) {
        values[input.name] = input.value;
        return values;
      }, {});
      console.log(data);
      console.log(formdata);
    },
    isRequired: function () {
      if (document.querySelector("#fullname").value.trim().length === 0) {
        this.selectived = true;
        this.nameMessage = "Vui lòng nhập trường này";
      } else {
        this.selectived = false;
        this.message = "";
      }
    },
    // isEmail: function(){
    //     var a = true;
    //     if( this.regex.test(document.querySelector('#email').value)===false ){
    //     this.emailForm = a;
    //     this.emailMessage=' trường này phải là email '
    //     } else {
    //     this.emailForm = false;
    //     this.emailMessage='';
    //     }
    // },
    isPass: function () {
      if (document.querySelector("#password").value.trim().length < 6) {
        this.passwordForm = true;
        this.passwordMessage = "vui lòng nhập mật khẩu trên 6 kí tự";
      } else {
        this.passwordForm = false;
        this.passwordMessage = "";
      }
    },
    isConfirm: function () {
      var passValue = document.querySelector("#form-1 #password").value;
      var confirmValue = document.querySelector(
        "#form-1 #password_confirmation"
      ).value;
      if (confirmValue.length !== 0 && confirmValue === passValue) {
        this.confirmForm = false;
        this.confirmMessage = "";
      } else {
        this.confirmForm = true;
        this.confirmMessage = "Mật khẩu nhập vào không chính xác";
      }
    },
    nameForcus: function () {
      this.selectived = false;
      this.nameMessage = "";
    },
    emailForcus: function () {
      this.emailForm = false;
      this.emailMessage = "";
    },
    passwordForcus: function () {
      this.passwordForm = false;
      this.passwordMessage = "";
    },
    confirmForcus: function () {
      this.confirmForm = false;
      this.confirmMessage = "";
    },
    handlePhoneInput: function (e) {
      this.phoneForm = false;
      this.phoneMessage = "";
      console.log(e);
      let input = e.target.value;
      input = input.replace(/-/g, "");

      const chunk = [];

      for (let i = 0; i < 9; i += 3) {
        const piece = input.substr(i, 3);

        if (piece.length < 3) {
          continue;
        }

        chunk.push(piece);
      }

      this.formattedPhoneNumber = chunk.join("-");
    },
  },
};
</script>

<style>
.main {
  background: #f1f1f1;
  min-height: 100vh;
  display: flex;
  justify-content: center;
}
.form {
  width: 360px;
  min-height: 100px;
  padding: 32px 24px;
  text-align: center;
  background: #fff;
  border-radius: 2px;
  margin: 24px;
  align-self: center;
  box-shadow: 0 2px 5px 0 rgba(51, 62, 73, 0.1);
}
.form .heading {
  font-size: 2rem;
}
.form .desc {
  text-align: center;
  color: #636d77;
  font-size: 1.6rem;
  font-weight: lighter;
  line-height: 2.4rem;
  margin-top: 16px;
  font-weight: 300;
}

.form-group {
  display: flex;
  margin-bottom: 16px;
  flex-direction: column;
}

.form-label,
.form-message {
  text-align: left;
}

.form-label {
  font-weight: 700;
  padding-bottom: 6px;
  line-height: 1.8rem;
  font-size: 1.4rem;
}

.form-control {
  height: 40px;
  padding: 8px 12px;
  border: 1px solid #b3b3b3;
  border-radius: 3px;
  outline: none;
  font-size: 1.4rem;
}

.form-control:hover {
  border-color: #1dbfaf;
}

.form-group.invalid .form-control {
  border-color: #f33a58;
}

.form-group.invalid .form-message {
  color: #f33a58;
}

.form-message {
  font-size: 1.2rem;
  line-height: 1.6rem;
  padding: 4px 0 0;
}
.form-group .phone-area {
  display: grid;
  grid-template-columns: 17% 83%;
}
.form-submit {
  outline: none;
  background-color: #1dbfaf;
  margin-top: 12px;
  padding: 12px 16px;
  font-weight: 600;
  color: #fff;
  border: none;
  width: 100%;
  font-size: 14px;
  border-radius: 8px;
  cursor: pointer;
}

.form-submit:hover {
  background-color: #1ac7b6;
}

.spacer {
  margin-top: 36px;
}
</style>