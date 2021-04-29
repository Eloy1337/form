<template>
  <form method="POST" class="form" novalidate @submit.prevent="submitHandler">
    <fieldset class="form__basic form__fieldset">
      <legend class="form__legend">Основная информация</legend>
      <div class="form__fio">
        <span class="form__title">ФИО</span>
        <div class="placeholder-container">
          <input
            type="text"
            placeholder=" "
            name="surname"
            autocomplete="off"
            required
            autofocus
            v-model.trim="surname"
            :class="{
              invalid: $v.surname.$dirty && !$v.surname.required,
            }"
          />
          <label>Фамилия</label>
          <small
            class="helper-text"
            v-if="$v.surname.$dirty && !$v.surname.required"
            >Заполните поле</small
          >
        </div>
        <div class="placeholder-container">
          <input
            type="text"
            placeholder=" "
            autocomplete="off"
            name="name"
            required
            v-model.trim="name"
            :class="{ invalid: $v.name.$dirty && !$v.name.required }"
          />
          <label>Имя</label>
          <small class="helper-text" v-if="$v.name.$dirty && !$v.name.required"
            >Заполните поле</small
          >
        </div>
        <div class="placeholder-container">
          <input
            type="text"
            placeholder=" "
            autocomplete="off"
            name="patronymic"
          />
          <label>Отчество</label>
        </div>
      </div>
      <div class="form__birthDate">
        <span class="form__title required">Дата рождения</span>
        <input
          type="date"
          name="birthDate"
          autocomplete="off"
          required
          v-model.trim="birthDate"
          :class="{
            invalid: $v.birthDate.$dirty && !$v.birthDate.required,
          }"
        />
        <small
          class="helper-text"
          v-if="$v.birthDate.$dirty && !$v.birthDate.required"
          >Заполните поле</small
        >
      </div>
      <div class="form__gender">
        <span class="form__title">Пол</span
        ><input
          type="radio"
          name="gender"
          id="gender-male"
          value="male"
        /><label for="gender-male">Муж</label
        ><input
          type="radio"
          name="gender"
          id="gender-female"
          value="female"
        /><label for="gender-female">Жен</label>
      </div>
      <div class="form__phone">
        <span class="form__title">Номер телефона</span>
        <div class="placeholder-container">
          <input
            name="phone"
            type="tel"
            autocomplete="off"
            placeholder=" "
            required
            v-model.trim="phone"
            :class="{
              invalid:
                ($v.phone.$dirty && !$v.phone.required) ||
                ($v.phone.$dirty && !$v.phone.numeric) ||
                ($v.phone.$dirty && !$v.phone.minLength) ||
                ($v.phone.$dirty && !$v.phone.maxLength),
            }"
          />
          <label>79876543210</label>
          <small
            class="helper-text"
            v-if="$v.phone.$dirty && !$v.phone.required"
            >Заполните поле</small
          >
          <small
            class="helper-text"
            v-else-if="
              ($v.phone.$dirty && !$v.phone.numeric) ||
              ($v.phone.$dirty && !$v.phone.minLength) ||
              ($v.phone.$dirty && !$v.phone.maxLength)
            "
            >Введите корректный номер телефона</small
          >
        </div>
      </div>
      <div class="form__group">
        <span class="form__title required">Группа клиентов</span>
        <select
          name="group"
          size="3"
          multiple
          required
          v-model.trim="group"
          :class="{
            invalid: $v.group.$dirty && !$v.group.required,
          }"
        >
          <option value="VIP">VIP</option>
          <option value="Проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select>
        <small class="helper-text" v-if="$v.group.$dirty && !$v.group.required"
          >Заполните поле</small
        >
      </div>
      <div class="form__doctor">
        <span class="form__title">Лечащий врач</span>
        <select name="doctor">
          <option value="Иванов">Иванов</option>
          <option value="Проблемные">Захаров</option>
          <option value="Чернышева">Чернышева</option>
        </select>
      </div>
      <div class="form__sms">
        <input type="checkbox" name="sms" id="sms" />
        <label for="sms">Не отправлять СМС</label>
      </div>
    </fieldset>
    <fieldset class="form__address form__fieldset">
      <legend class="form__legend">Адрес</legend>
      <div class="form__country">
        <div class="placeholder-container">
          <input type="text" placeholder=" " name="country" />
          <label>Страна</label>
        </div>
      </div>
      <div class="form__area">
        <div class="placeholder-container">
          <input type="text" placeholder=" " name="area" />
          <label>Область</label>
        </div>
      </div>
      <div class="form__city">
        <div class="placeholder-container">
          <input
            type="text"
            placeholder=" "
            name="city"
            required
            v-model.trim="city"
            :class="{
              invalid: $v.city.$dirty && !$v.city.required,
            }"
          />
          <label>Город</label>
          <small class="helper-text" v-if="$v.city.$dirty && !$v.city.required"
            >Заполните поле</small
          >
        </div>
      </div>
      <div class="form__street">
        <div class="placeholder-container">
          <input type="text" placeholder=" " name="street" />
          <label>Улица</label>
        </div>
      </div>
      <div class="form__house">
        <div class="placeholder-container">
          <input type="text" placeholder=" " name="house" />
          <label>Дом</label>
        </div>
      </div>
      <div class="form__index">
        <div class="placeholder-container">
          <input
            type="number"
            placeholder=" "
            name="index"
            v-model.trim="index"
            :class="{
              invalid:
                ($v.index.$dirty && !$v.index.numeric) ||
                ($v.index.$dirty && !$v.index.minLength) ||
                ($v.index.$dirty && !$v.index.maxLength),
            }"
          />
          <label>Индекс</label>
          <small
            class="helper-text"
            v-if="
              ($v.index.$dirty && !$v.index.numeric) ||
              ($v.index.$dirty && !$v.index.minLength) ||
              ($v.index.$dirty && !$v.index.maxLength)
            "
            >Введите корректный индекс</small
          >
        </div>
      </div>
    </fieldset>
    <fieldset class="form__passport form__fieldset">
      <legend class="form__legend">Паспорт</legend>
      <div class="form__document">
        <span class="form__title required">Тип документа</span>
        <select
          name="document"
          required
          v-model.trim="document"
          :class="{
            invalid: $v.document.$dirty && !$v.document.required,
          }"
        >
          <option value="Паспорт">Паспорт</option>
          <option value="Свидетельство о рождении">
            Свидетельство о рождении
          </option>
          <option value="Вод. удостоверение">Вод. удостоверение</option>
        </select>
        <small
          class="helper-text"
          v-if="$v.document.$dirty && !$v.document.required"
          >Заполните поле</small
        >
      </div>
      <div class="form__series">
        <div class="placeholder-container">
          <input
            pattern="[0-9]{4}"
            type="text"
            autocomplete="off"
            placeholder=" "
            name="series"
            v-model.trim="series"
            :class="{
              invalid:
                ($v.series.$dirty && !$v.series.numeric) ||
                ($v.series.$dirty && !$v.series.minLength) ||
                ($v.series.$dirty && !$v.series.maxLength),
            }"
          />
          <label>Серия</label>
          <small
            class="helper-text"
            v-if="
              ($v.series.$dirty && !$v.series.numeric) ||
              ($v.series.$dirty && !$v.series.minLength) ||
              ($v.series.$dirty && !$v.series.maxLength)
            "
            >Введите корректное значение серии</small
          >
        </div>
      </div>
      <div class="form__number">
        <div class="placeholder-container">
          <input
            pattern="[0-9]{6}"
            type="text"
            autocomplete="off"
            placeholder=" "
            name="number"
            v-model.trim="number"
            :class="{
              invalid:
                ($v.number.$dirty && !$v.number.numeric) ||
                ($v.number.$dirty && !$v.number.minLength) ||
                ($v.number.$dirty && !$v.number.maxLength),
            }"
          />
          <label>Номер</label>
          <small
            class="helper-text"
            v-if="
              ($v.number.$dirty && !$v.number.numeric) ||
              ($v.number.$dirty && !$v.number.minLength) ||
              ($v.number.$dirty && !$v.number.maxLength)
            "
            >Введите корректное значение номера</small
          >
        </div>
      </div>
      <div class="form__place">
        <div class="placeholder-container">
          <input type="text" autocomplete="off" placeholder=" " name="place" />
          <label>Кем выдан</label>
        </div>
      </div>
      <div class="form__issueDate">
        <span class="form__title required">Дата выдачи</span>
        <input
          type="date"
          autocomplete="off"
          name="issueDate"
          required
          v-model.trim="issueDate"
          :class="{
            invalid: $v.issueDate.$dirty && !$v.issueDate.required,
          }"
        />
        <small
          class="helper-text"
          v-if="$v.issueDate.$dirty && !$v.issueDate.required"
          >Заполните поле</small
        >
      </div>
    </fieldset>
    <div class="form__submit">
      <input type="submit" value="Отправить" />
    </div>
  </form>
</template>

<script>
import {
  required,
  minLength,
  maxLength,
  numeric,
} from "vuelidate/lib/validators";

export default {
  name: "MyForm",
  data: () => ({
    success: false,
    surname: "",
    name: "",
    birthDate: "",
    phone: "7",
    group: [],
    city: "",
    document: "",
    issueDate: "",
    index: "",
    series: "",
    number: "",
  }),
  validations: {
    surname: { required },
    name: { required },
    birthDate: { required },
    phone: {
      required,
      numeric,
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    group: { required },
    city: { required },
    document: { required },
    issueDate: { required },
    index: { numeric, minLength: minLength(6), maxLength: maxLength(6) },
    series: { numeric, minLength: minLength(4), maxLength: maxLength(4) },
    number: { numeric, minLength: minLength(6), maxLength: maxLength(6) },
  },
  methods: {
    submitHandler() {
      if (this.$v.$invalid) {
        this.$v.$touch();
      } else {
        this.success = true;
        this.$emit("success", this.success);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$primaryColor: #5596d3;
$maxWidthContainer: 1170;
$md1: $maxWidthContainer + 12;
$md2: 991.98;
$md3: 767.98;
$md4: 479.98;

.form {
  input,
  input[type="radio"] + label,
  input[type="checkbox"] + label:before,
  select option,
  select {
    box-sizing: border-box;
    color: #000;
    font-size: 1.6rem;
    line-height: 1.6rem;
    outline: 0;
    padding: 1.5rem 2rem;
    width: 100%;
    background-color: #f9f9f9;
    border: 1px solid #e5e5e5;
    border-radius: 3px;
    -webkit-transition: 0.35s ease-in-out;
    -moz-transition: 0.35s ease-in-out;
    -o-transition: 0.35s ease-in-out;
    transition: 0.35s ease-in-out;
    transition: all 0.35s ease-in-out;
  }

  input[type="checkbox"] {
    display: none;

    & + label {
      position: relative;
      display: block;
      padding-left: 1.6em;
      margin-bottom: 2rem;
      cursor: pointer;
      color: black;

      &::before {
        position: absolute;
        // top: 0.2rem;
        display: block;
        margin: auto;
        top: 0;
        bottom: 0;
        left: 0;
        display: block;
        width: 2rem;
        height: 2rem;
        padding: 0;
        content: "";
      }

      &::after {
        position: absolute;
        border-radius: 5px;
        text-align: center;
        margin: auto;
        top: 0;
        bottom: 0;
        left: 0;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 2rem;
        height: 2rem;
        font-size: 1.2rem;
        background-color: $primaryColor;
        color: #fff;
        opacity: 0;
        font-family: FontAwesome;
        content: "\f00c";
      }
    }

    &:checked + label:after {
      opacity: 1;
    }
  }

  input,
  select {
    position: relative;
  }

  input:required + label::after {
    content: "*";
    font-size: 1.5rem;
    color: red;
    position: absolute;
    top: 0;
    right: 0.5rem;
    display: block;
  }

  input:focus,
  select:focus {
    outline: none;
    border: 1px solid $primaryColor;
  }

  .helper-text {
    color: darken(red, 5%);
  }

  .invalid {
    border: 1px solid red !important;
  }

  .required {
    display: inline-block;
    position: relative;
    width: auto;

    &::after {
      content: "*";
      font-size: 1.5rem;
      color: red;
      position: absolute;
      top: 0;
      right: -1rem;
      display: block;
    }
  }

  // &__basic {
  // }

  &__legend {
    color: #000;
    font-size: 2rem;
    padding: 1.5rem;
    border: solid 2px rgba($primaryColor, 0.4);
    border-radius: 10px;
    margin-bottom: 2rem;
  }

  &__fio {
    width: 100%;

    > * {
      margin-bottom: 2rem;
    }
  }

  &__fieldset {
    > *:not(legend) {
      width: 100%;
      margin-bottom: 2rem;
    }

    border: solid 2px rgba($primaryColor, 0.4);
    border-radius: 10px;
    margin-top: 2rem;
    padding: 0 2rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  &__title {
    color: $primaryColor;
    display: block;
    font-weight: bold;
    margin-bottom: 2rem;
  }

  &__birthDate {
    width: 49% !important;

    @media (max-width: $md4 + px) {
      width: 100% !important;
    }
  }

  &__gender {
    width: 49% !important;

    @media (max-width: $md4 + px) {
      width: 100% !important;
    }

    label {
      margin-bottom: 2rem;
    }

    input[type="radio"] {
      display: none;

      &:checked + label {
        background-color: $primaryColor;
        color: #fff;
        border-color: darken($primaryColor, 20%);
      }
    }

    input[type="radio"] + label:first-of-type {
      border-top-left-radius: 3px;
      border-bottom-left-radius: 3px;
    }

    input[type="radio"] + label:last-of-type {
      border-top-right-radius: 3px;
      border-bottom-right-radius: 3px;
    }

    input[type="radio"] + label {
      display: inline-block;
      width: 49%;
      text-align: center;
      border-radius: 0;

      box-sizing: border-box;
      color: #000;
      font-size: 1.6rem;
      line-height: 1.6rem;
      outline: 0;
      padding: 1.8rem 2rem;
    }
  }

  &__phone {
    width: 100%;
  }

  &__group {
    width: 100%;

    select {
      overflow: hidden;
      padding: 0rem 0rem;
    }
  }

  &__doctor {
    width: 100%;
  }

  &__sms {
    width: 100%;
  }

  // &__address {
  // }

  // &__country {
  // }

  // &__area {
  // }

  // &__city {
  // }

  // &__street {
  // }

  // &__house {
  // }

  // &__index {
  // }

  // &__passport {
  // }

  &__document {
    position: relative;
  }

  // &__series {
  // }

  // &__number {
  // }

  // &__place {
  // }

  // &__issueDate {
  // }

  &__submit {
    margin-top: 2rem;

    input {
      font-size: 1.5rem;
      background-color: $primaryColor;
      color: #fff;
      border-color: darken($primaryColor, 20%);
    }
  }
}

.placeholder-container {
  position: relative;
  width: 100%;
  // margin-bottom: 2rem;

  input {
    box-sizing: border-box;
    color: #000;
    font-size: 1.6rem;
    line-height: 1.6rem;
    outline: 0;
    padding: 1.5rem 2rem;
    width: 100%;

    &:focus {
      border: 1px solid $primaryColor;
    }
  }

  label {
    color: #000;
    font-size: 16px;
    line-height: 16px;
    padding: 5px 10px;
    pointer-events: none;
    position: absolute;
    transition: all 200ms;
    top: 12px;
    left: 10px;
    opacity: 0.5;
  }

  input:focus + label,
  input:not(:placeholder-shown) + label {
    top: -1rem;
    left: 1rem;
    font-size: 1.1rem;
    background-color: white;
    border: 1px solid $primaryColor;
    border-radius: 1rem;
    padding: 0.2rem 1rem;
    opacity: 1;
  }
}
</style>
