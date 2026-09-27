<script setup lang="ts">
import userData from '@/data/user.json'
import { ref } from 'vue'

defineOptions({
  name: 'UsersList',
})

interface User {
  id: number
  gender: 'male' | 'female'
  name: {
    title: string
    first: string
    last: string
  }
  location: {
    street: {
      number: number
      name: string
    }
    city: string
    state: string
    country: string
    postcode: number | string
  }
  email: string
  dob: {
    date: string
    age: number
  }
  phone: string
  cell: string
  picture: string
  hobbies: string[]
  details: string
}

const user = userData as User

const fullName = `${user.name.title}. ${user.name.first} ${user.name.last}`
const birthDate = new Intl.DateTimeFormat('uk-UA').format(new Date(user.dob.date))
const genderLabel = user.gender === 'female' ? 'Жінка' : 'Чоловік'
const areDetailsVisible = ref(false)
</script>

<template>
  <article
    class="user-card"
    :class="{
      minor: user.dob.age < 18,
      young: user.dob.age >= 18 && user.dob.age <= 30,
      adult: user.dob.age >= 31 && user.dob.age <= 50,
      senior: user.dob.age > 50,
    }"
  >
    <img class="user-photo" v-bind:src="user.picture" v-bind:alt="`Фото ${fullName}`" />

    <section class="user-content">
      <p class="user-label">Профіль користувача</p>
      <h1>{{ fullName }}</h1>

      <dl class="user-details">
        <div class="user-row">
          <dt>Стать</dt>
          <dd>{{ genderLabel }}</dd>
        </div>
        <div class="user-row">
          <dt>Дата народження</dt>
          <dd>
            {{ birthDate }}
            <span v-if="user.dob.age > 18">({{ user.dob.age }} років)</span>
          </dd>
        </div>
        <div class="user-row">
          <dt>Адреса</dt>
          <dd>
            {{ user.location.street.number }} {{ user.location.street.name }},
            {{ user.location.city }}, {{ user.location.state }},
            {{ user.location.country }}
          </dd>
        </div>
        <div class="user-row">
          <dt>Email</dt>
          <dd>{{ user.email }}</dd>
        </div>
        <div class="user-row">
          <dt>Телефон</dt>
          <dd>{{ user.phone }}</dd>
        </div>
      </dl>
      <section class="hobbies">
        <h2>Хобі</h2>

        <ul class="hobby-list">
          <li v-for="hobby in user.hobbies" :key="hobby">
            {{ hobby }}
          </li>
        </ul>
      </section>

      <section class="additional-info">
        <button
          type="button"
          :aria-expanded="areDetailsVisible"
          @click="areDetailsVisible = !areDetailsVisible"
        >
          {{ areDetailsVisible ? 'Приховати деталі' : 'Показати деталі' }}
        </button>

        <p v-show="areDetailsVisible">
          {{ user.details }}
        </p>
      </section>
    </section>
  </article>
</template>

<style scoped>
.user-card {
  display: grid;
  grid-template-columns: 240px 1fr;
  width: min(100%, 850px);
  overflow: hidden;
  background: #ffffff;
  border: 1px solid #dbe4f0;
  border-radius: 8px;
  box-shadow: 0 16px 40px rgb(30 50 80 / 12%);
}

.user-photo {
  width: 100%;
  height: 100%;
  min-height: 340px;
  object-fit: cover;
}

.user-content {
  padding: 32px;
}

.user-label {
  margin: 0 0 8px;
  color: #087f5b;
  font-weight: 700;
}

h1 {
  margin: 0;
  color: #14213d;
  font-size: 32px;
}

.user-details {
  display: grid;
  gap: 14px;
  margin: 28px 0 0;
}

.user-row {
  display: grid;
  grid-template-columns: 140px 1fr;
  gap: 16px;
  padding-bottom: 12px;
  border-bottom: 1px solid #e5eaf1;
}

dt {
  color: #64748b;
}

dd {
  margin: 0;
  color: #172554;
}

.user-card {
  border-left: 6px solid transparent;
}

.user-card.minor {
  border-left-color: #eab308;
}

.user-card.young {
  border-left-color: #16a34a;
}

.user-card.adult {
  border-left-color: #2563eb;
}

.user-card.senior {
  border-left-color: #9333ea;
}

.hobbies,
.additional-info {
  margin-top: 24px;
}

.hobbies h2 {
  margin-bottom: 12px;
  font-size: 18px;
}

.hobby-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  padding: 0;
  list-style: none;
}

.hobby-list li {
  padding: 6px 12px;
  background: #eef2f7;
  border-radius: 6px;
}

.additional-info button {
  padding: 10px 16px;
  color: #ffffff;
  background: #172554;
  border: 0;
  border-radius: 6px;
  cursor: pointer;
}

.additional-info p {
  margin: 16px 0 0;
  line-height: 1.6;
}

@media (max-width: 650px) {
  .user-card {
    grid-template-columns: 1fr;
  }

  .user-photo {
    height: 280px;
  }

  .user-row {
    grid-template-columns: 1fr;
    gap: 4px;
  }
}
</style>
