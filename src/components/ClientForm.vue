<template>
  <div class="container pt-1">
    <div class="card">
      <h1>Добавьте нового клиента</h1>
      <div class="form-control">
        <div class="card center">
          <h4>Фамилия</h4>
          <input type="text" v-model="l_name"/>
          <span v-if="v$.l_name.$error">{{ v$.l_name.$errors[0].$message }}</span>
          <h4>Имя</h4>
          <input type="text" v-model="name"/>
          <span v-if="v$.name.$error">{{ v$.name.$errors[0].$message }}</span>
          <h4>Отчество</h4>
          <input type="text"/>
        </div>
        <div class="card center">
          <h4>Дата рождения:</h4>
          <input type="date" class="date" name="date" v-model="birthday"/>
          <span v-if="v$.birthday.$error">{{ v$.birthday.$errors[0].$message }}</span>
          <h4>Номер телефона</h4>
          <input type="tel" v-model="tel">
          <span v-if="v$.tel.$error">{{ v$.tel.$errors[0].$message }}</span>
        </div>
        <div class="card center">
          <h4>Выберите пол</h4>
          <input type="radio" id="male" value="Мужской" name="gender">
          <label for="male">Мужской</label>
          <input type="radio" id="female" value="Женский" name="gender">
          <label for="female">Женский</label>
        </div>
        <div class="card center">
          <h4>Группа клиентов</h4>
          <select multiple v-model="group">
            <option>VIP</option>
            <option>Проблемные</option>
            <option>ОМС</option>
          </select>
          <span v-if="v$.group.$error">{{ v$.group.$errors[0].$message }}</span>
          <h4>Лечащий врач</h4>
          <select v-model="doctor">
            <option disabled value="">Выберите один из вариантов</option>
            <option>Иванов И.</option>
            <option>Захаров В.</option>
            <option>Чернышева Л.</option>
          </select>
          <span v-if="v$.doctor.$error">{{ v$.doctor.$errors[0].$message }}</span>
        </div>
        <div class="card center">
          <h4>Уведомление</h4>
          <input type="checkbox" id="checkbox">
          <label for="checkbox">Не отправлять СМС</label>
        </div>
      </div>
    </div>
  </div>
  <div class="container pt-1">
    <div class="card">
      <h1>Адрес проживания</h1>
      <div class="form-control">
        <div class="card center">
          <h4>Почтовый индекс</h4>
          <input type="text">
          <h4>Страна</h4>
          <input type="text">
          <h4>Область</h4>
          <input type="text"></div>
        <div class="card center">
          <h4>Город</h4>
          <input type="text" v-model="city">
          <span v-if="v$.city.$error">{{ v$.city.$errors[0].$message }}</span>
          <h4>Улица</h4>
          <input type="text">
          <h4>Дом</h4>
          <input type="text"></div>
      </div>
    </div>
  </div>
  <div class="container pt-1">
    <div class="card">
      <h1>Документ, удостоверяющий личность</h1>
      <div class="form-control">
        <div class="card center">
          <h4>Тип документа</h4>
          <select v-model="doctype">
            <option disabled value="">Выберите один из вариантов</option>
            <option>Паспорт</option>
            <option>Свидетельство о рождении</option>
            <option>Водительское удостоверение</option>
          </select>
          <span v-if="v$.doctype.$error">{{ v$.doctype.$errors[0].$message }}</span>
          <h4>Серия/Номер</h4>
          <input type="text" id="serial_1"/>
          <input type="text" id="number"/>
        </div>
        <div class="card center">
          <h4>Кем выдан</h4>
          <input type="textarea"/>
          <h4>Дата выдачи:</h4>
          <input type="date" name="date" class="date" v-model="docgiven"/>
          <span v-if="v$.docgiven.$error">{{ v$.docgiven.$errors[0].$message }}</span>
        </div>
      </div>
    </div>
  </div>
  <div class="container">
    <button class="btn" @click="submitForm">Создать пользователя</button>
  </div>
</template>

<script>
import useValidate from '@vuelidate/core'
import { maxLength, required } from '@vuelidate/validators'

export default {
  data () {
    return {
      v$: useValidate(),
      l_name: '',
      name: '',
      birthday: '',
      tel: '',
      group: [],
      doctor: '',
      city: '',
      doctype: '',
      docgiven: ''
    }
  },
  validations () {
    return {
      l_name: { required },
      name: { required },
      birthday: { required },
      tel: { required, maxLength: maxLength(11) },
      group: { required },
      doctor: { required },
      city: { required },
      doctype: { required },
      docgiven: { required }
    }
  },
  methods: {
    submitForm () {
      this.v$.$validate()
      if (!this.v$.$error) {
        alert('Клиент успешно создан!')
      } else {
        alert('Необходимо правильно заполнить все поля')
      }
      console.log(this.v$.$error)
    }
  }
}
</script>
