
<script>
import { validationMixin } from 'vuelidate'
import { required } from 'vuelidate/lib/validators'
import './/assets/style.sass'

export default {
  mixins: [validationMixin],
  data() {
    return {
      form: {
        client: '',
        tel: '',
        birthday: '',
        issueDate: '',
        city: '',
        surname: '',
        name: '',
        patronymic: '',
        doctor: 'Ivanov',
        sendSms: false,
        documentType: ''
      },
      doctors: [
        {
          label: 'Иванов',
          value: 'Ivanov'
        },
        {
          label: 'Захаров',
          value: 'Zakharov'
        },
        {
          label: 'Чернышева',
          value: 'Chernysheva'
        }
      ],
      clientsGroup: [
        {
          label: 'VIP',
          value: 'VIP'
        },
        {
          label: 'Проблемные',
          value: 'Problematic'
        },
        {
          label: 'ОМС',
          value: 'OMS'
        },
      ],
      documentTypes: [
        {
          label: 'Паспорт',
          value: 'Passport'
        },
        {
          label: 'Свидетельство о рождении',
          value: 'Birth certificate'
        },

        {
          label: 'Вод. удостоверение',
          value: 'Drivers license'
        },

      ],
      themes: [
        {
          label: 'Технологии',
          value: 'IT'
        },
        {
          label: 'Языки',
          value: 'languages'
        },
        {
          label: 'Математика',
          value: 'mathematics'
        },
        {
          label: 'История',
          value: 'history'
        }
      ]
    }
  },
  validations: {
    form: {
      surname: { required },
      birthday: { required },
      name: { required },
      tel: { required },
      city: { required },
      issueDate: { required },
      documentType: { required },
      client: {
        minCount(value) {
          return value.length !== 0
        }
      }
    }
  },
  methods: {
    checkForm() {
      this.$v.form.$touch()
      if (!this.$v.form.$error) {
        alert("Новый клиент успешно создан!")
      }
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <form class="form-inputs" @submit.prevent="checkForm">



      <div class="clients-information field">

        <h1 class="title">Данные клиента</h1>
        <div class="form-info">
          <label for="surname">Фамилия*</label>
          <input id="surname" class="surname" :class="$v.form.surname.$error ? 'is-invalid' : ''"
            v-model.trim="form.surname">
          <p v-if="$v.form.surname.$dirty && !$v.form.surname.required" class="invalid-feedback">Поле обязательно для
            заполнения
          </p>
        </div>

        <div class="form-info">
          <label for="name">Имя*</label>
          <input id="name" class="name" :class="$v.form.name.$error ? 'is-invalid' : ''" v-model.trim="form.name">
          <p v-if="$v.form.name.$dirty && !$v.form.name.required" class="invalid-feedback">Поле обязательно для заполнения
          </p>
        </div>

        <div class="form-info">
          <label for="patronymic">Отчество</label>
          <input id="patronymic" v-model.trim="form.patronymic">
        </div>

        <div class="form-info">
          <label for="birthday">Дата рождения*</label>
          <input type="date" id="birthday" class="birthday" :class="$v.form.birthday.$error ? 'is-invalid' : ''"
            v-model="form.birthday">
          <p v-if="$v.form.birthday.$dirty && !$v.form.birthday.required" class="invalid-feedback">Поле обязательно для
            заполнения
          </p>
        </div>

        <div class="form-info tel_box">
          <label for="tel">Номер телефона*</label>
          <span class="code">+7
          <input type="text" class="number-phone" :class="$v.form.tel.$error ? 'is-invalid' : ''" v-model="form.tel"
            id="tel" maxlength="10" name="phone" pattern="[0-9]{10}">
          </span><p v-if="$v.form.tel.$dirty && !$v.form.tel.required" class="invalid-feedback">Поле обязательно для
            заполнения
          </p>
        </div>

        <div class="form-info">
          <label for="sex">Пол</label>
          <input id="sex">
        </div>

        <div class="form-info">
          <label for="clients">Группа клиентов*</label>
          <select id="clients" class="clients" :class="$v.form.client.$error ? 'is-invalid' : ''" v-model="form.client"
            multiple>
            <option v-for="(client, index) in clientsGroup" :value="client.value" :key="index">{{
              client.label }}</option>
          </select>
          <p v-if="$v.form.client.$dirty && !$v.form.client.minCount" class="invalid-feedback">
            Выберете группу!
          </p>
        </div>

        <div class="form-info">
          <label for="doctor">Лечащий врач</label>
          <select id="doctor" v-model="doctor">
            <option v-for="(doctor, index) in doctors" :value="doctor.value" :key="index">{{ doctor.label }}</option>
          </select>
        </div>

        <div class="form-info send-sms-box">
          <input id="send-sms" type="checkbox" class="check" v-model="sendSms">
          <label for="send-sms">Не отправлять СМС</label>
        </div>

      </div>

      <div class="clients-adress-info field">
        <h1 class="title">Адрес</h1>

        <div class="form-info">
          <label for="index">Индекс</label>
          <input id="index">
        </div>

        <div class="form-info">
          <label for="country">Страна</label>
          <input id="country">
        </div>

        <div class="form-info">
          <label for="region">Область</label>
          <input id="region">
        </div>
        <div class="form-info">
          <label for="city">Город*</label>
          <input id="city" class="city" :class="$v.form.city.$error ? 'is-invalid' : ''" v-model="form.city">
          <p v-if="$v.form.city.$dirty && !$v.form.city.required" class="invalid-feedback">Поле обязательно для
            заполнения
          </p>
        </div>


        <div class="form-info">
          <label for="street">Улица</label>
          <input id="street">
        </div>

        <div class="form-info">
          <label for="house">Дом</label>
          <input id="house">
        </div>
      </div>
      <div class="clients-documents field">
        <h1 class="title">Документы</h1>

        <div class="form-info">
          <label for="document">Тип документа*</label>
          <select id="document" class="document" :class="$v.form.documentType.$error ? 'is-invalid' : ''"
            v-model="form.documentType">
            <option v-for="(documentType, index) in documentTypes" :value="documentType.value" :key="index">{{
              documentType.label }}</option>
          </select>
          <p v-if="$v.form.documentType.$dirty && !$v.form.documentType.required" class="invalid-feedback">
            Выберете тип документа!
          </p>
        </div>

        <div class="form-info">
          <label for="series">Серия</label>
          <input id="series">
        </div>

        <div class="form-info">
          <label for="number">Номер</label>
          <input id="number">
        </div>

        <div class="form-info">
          <label for="issued-by">Кем выдан</label>
          <input id="issued-by">
        </div>


        <div class="form-info">
          <label for="issue-date">Дата выдачи*</label>
          <input type="date" id="issue-date" class="issue-date" :class="$v.form.issueDate.$error ? 'is-invalid' : ''"
            v-model="form.issueDate">
          <p v-if="$v.form.issueDate.$dirty && !$v.form.issueDate.required" class="invalid-feedback">Поле обязательно для
            заполнения
          </p>
        </div>

        <div class="form-info button">
          <button type="submit" class="button-create">Создать клиента</button>
        </div>

      </div>
    </form>
  </div>
</template>

<style lang="scss" scoped></style>

