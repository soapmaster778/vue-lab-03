<script setup lang="ts">
import { ref } from 'vue'
import userData from '@/data/user.json'

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

interface UserSeed {
  id: number
  gender: User['gender']
  title: string
  first: string
  last: string
  city: string
  state: string
  country: string
  date: string
  age: number
  email: string
  phone: string
  picture: string
  hobbies: string[]
  details: string
}

const baseUser = userData as User

const userSeeds: UserSeed[] = [
  {
    id: 2,
    gender: 'male',
    title: 'Mr',
    first: 'Oliver',
    last: 'Smith',
    city: 'London',
    state: 'England',
    country: 'United Kingdom',
    date: '2009-01-14T10:00:00.000Z',
    age: 17,
    email: 'oliver.smith@example.com',
    phone: '020-123-4567',
    picture: '/users/user-2.jpg',
    hobbies: ['Футбол', 'Ігри', 'Кіно'],
    details: 'Олівер навчається у школі та захоплюється футболом.',
  },
  {
    id: 3,
    gender: 'female',
    title: 'Ms',
    first: 'Sofia',
    last: 'Rossi',
    city: 'Rome',
    state: 'Lazio',
    country: 'Italy',
    date: '2008-04-22T10:00:00.000Z',
    age: 18,
    email: 'sofia.rossi@example.com',
    phone: '06-555-0103',
    picture: '/users/user-3.jpg',
    hobbies: ['Малювання', 'Музика'],
    details: 'Софія вивчає дизайн і любить сучасне мистецтво.',
  },
  {
    id: 4,
    gender: 'male',
    title: 'Mr',
    first: 'Noah',
    last: 'Martin',
    city: 'Paris',
    state: 'Île-de-France',
    country: 'France',
    date: '1992-07-03T10:00:00.000Z',
    age: 34,
    email: 'noah.martin@example.com',
    phone: '01-555-0104',
    picture: '/users/user-4.jpg',
    hobbies: ['Біг', 'Кулінарія'],
    details: 'Ноа працює розробником і бере участь у марафонах.',
  },
  {
    id: 5,
    gender: 'female',
    title: 'Ms',
    first: 'Amelia',
    last: 'Brown',
    city: 'Toronto',
    state: 'Ontario',
    country: 'Canada',
    date: '1984-02-19T10:00:00.000Z',
    age: 42,
    email: 'amelia.brown@example.com',
    phone: '416-555-0105',
    picture: '/users/user-5.jpg',
    hobbies: ['Читання', 'Йога'],
    details: 'Амелія викладає англійську мову та практикує йогу.',
  },
  {
    id: 6,
    gender: 'male',
    title: 'Mr',
    first: 'Liam',
    last: 'Wilson',
    city: 'Sydney',
    state: 'New South Wales',
    country: 'Australia',
    date: '1970-06-11T10:00:00.000Z',
    age: 56,
    email: 'liam.wilson@example.com',
    phone: '02-555-0106',
    picture: '/users/user-6.jpg',
    hobbies: ['Риболовля', 'Подорожі'],
    details: 'Ліам багато подорожує та фотографує природу.',
  },
  {
    id: 7,
    gender: 'female',
    title: 'Ms',
    first: 'Mia',
    last: 'Garcia',
    city: 'Madrid',
    state: 'Madrid',
    country: 'Spain',
    date: '1997-08-30T10:00:00.000Z',
    age: 29,
    email: 'mia.garcia@example.com',
    phone: '91-555-0107',
    picture: '/users/user-7.jpg',
    hobbies: ['Танці', 'Подорожі'],
    details: 'Міа працює фотографкою та займається танцями.',
  },
  {
    id: 8,
    gender: 'male',
    title: 'Mr',
    first: 'Ethan',
    last: 'Miller',
    city: 'Boston',
    state: 'Massachusetts',
    country: 'USA',
    date: '1977-03-27T10:00:00.000Z',
    age: 49,
    email: 'ethan.miller@example.com',
    phone: '617-555-0108',
    picture: '/users/user-8.jpg',
    hobbies: ['Велоспорт', 'Історія'],
    details: 'Ітан викладає історію та подорожує велосипедом.',
  },
  {
    id: 9,
    gender: 'female',
    title: 'Ms',
    first: 'Chloe',
    last: 'Dubois',
    city: 'Brussels',
    state: 'Brussels',
    country: 'Belgium',
    date: '1963-05-15T10:00:00.000Z',
    age: 63,
    email: 'chloe.dubois@example.com',
    phone: '02-555-0109',
    picture: '/users/user-9.jpg',
    hobbies: ['Садівництво', 'Читання'],
    details: 'Хлоя захоплюється садівництвом і класичною літературою.',
  },
  {
    id: 10,
    gender: 'male',
    title: 'Mr',
    first: 'Lucas',
    last: 'Novak',
    city: 'Prague',
    state: 'Prague',
    country: 'Czech Republic',
    date: '1995-09-01T10:00:00.000Z',
    age: 31,
    email: 'lucas.novak@example.com',
    phone: '02-555-0110',
    picture: '/users/user-10.jpg',
    hobbies: ['Музика', 'Походи'],
    details: 'Лукас працює музикантом і любить гірські походи.',
  },
]

const users: User[] = [
  {
    ...baseUser,
    picture: '/users/user-1.jpg',
  },
  ...userSeeds.map((seed) => ({
    ...baseUser,
    id: seed.id,
    gender: seed.gender,
    name: {
      title: seed.title,
      first: seed.first,
      last: seed.last,
    },
    location: {
      ...baseUser.location,
      street: {
        number: 100 + seed.id,
        name: 'Central Street',
      },
      city: seed.city,
      state: seed.state,
      country: seed.country,
      postcode: 10000 + seed.id,
    },
    email: seed.email,
    dob: {
      date: seed.date,
      age: seed.age,
    },
    phone: seed.phone,
    cell: seed.phone,
    picture: seed.picture,
    hobbies: seed.hobbies,
    details: seed.details,
  })),
]

const visibleDetails = ref<Record<number, boolean>>({})

function getFullName(user: User): string {
  return `${user.name.title}. ${user.name.first} ${user.name.last}`
}

function formatBirthDate(date: string): string {
  return new Intl.DateTimeFormat('uk-UA').format(new Date(date))
}

function getGenderLabel(gender: User['gender']): string {
  return gender === 'female' ? 'Жінка' : 'Чоловік'
}

function toggleDetails(userId: number): void {
  visibleDetails.value[userId] = !visibleDetails.value[userId]
}
</script>

<template>
  <section class="users-page">
    <div v-if="users.length > 0" class="users-list">
      <article
        v-for="user in users"
        :key="user.id"
        class="user-card"
        :class="{
          minor: user.dob.age < 18,
          young: user.dob.age >= 18 && user.dob.age <= 30,
          adult: user.dob.age >= 31 && user.dob.age <= 50,
          senior: user.dob.age > 50,
        }"
      >
        <img
          class="user-photo"
          v-bind:src="user.picture"
          v-bind:alt="`Фото ${getFullName(user)}`"
        />

        <section class="user-content">
          <h1>{{ getFullName(user) }}</h1>

          <dl class="user-details">
            <div class="user-row">
              <dt>Стать</dt>
              <dd>{{ getGenderLabel(user.gender) }}</dd>
            </div>

            <div class="user-row">
              <dt>Дата народження</dt>
              <dd>
                {{ formatBirthDate(user.dob.date) }}
                <span v-if="user.dob.age > 18"> ({{ user.dob.age }} років) </span>
              </dd>
            </div>

            <div class="user-row">
              <dt>Адреса</dt>
              <dd>
                {{ user.location.street.number }}
                {{ user.location.street.name }}, {{ user.location.city }},
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
              :aria-expanded="Boolean(visibleDetails[user.id])"
              @click="toggleDetails(user.id)"
            >
              {{ visibleDetails[user.id] ? 'Приховати деталі' : 'Показати деталі' }}
            </button>

            <p v-show="visibleDetails[user.id]">
              {{ user.details }}
            </p>
          </section>
        </section>
      </article>
    </div>

    <p v-else class="empty-message">Список юзерів пустий</p>
  </section>
</template>

<style scoped>
.users-page {
  width: 100%;
}

.users-list {
  display: grid;
  gap: 16px;
  justify-items: center;
}

.user-card {
  display: grid;
  grid-template-columns: 170px 1fr;
  width: min(100%, 720px);
  overflow: hidden;
  background: #ffffff;
  border: 1px solid #d8dee8;
  border-left: 4px solid transparent;
  border-radius: 6px;
}

.user-card.minor {
  border-left-color: #ca8a04;
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

.user-photo {
  width: 100%;
  height: 100%;
  min-height: 260px;
  object-fit: cover;
}

.user-content {
  padding: 20px;
}

h1 {
  margin: 0;
  color: #172554;
  font-size: 22px;
}

.user-details {
  display: grid;
  gap: 8px;
  margin: 18px 0 0;
}

.user-row {
  display: grid;
  grid-template-columns: 120px 1fr;
  gap: 12px;
  padding-bottom: 7px;
  border-bottom: 1px solid #e5e7eb;
}

dt {
  color: #64748b;
  font-size: 14px;
}

dd {
  margin: 0;
  overflow-wrap: anywhere;
  color: #1f2937;
  font-size: 14px;
}

.hobbies,
.additional-info {
  margin-top: 16px;
}

.hobbies h2 {
  margin: 0 0 8px;
  font-size: 16px;
}

.hobby-list {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  padding: 0;
  margin: 0;
  list-style: none;
}

.hobby-list li {
  padding: 4px 8px;
  background: #f1f5f9;
  border-radius: 4px;
  font-size: 13px;
}

.additional-info button {
  padding: 7px 11px;
  color: #172554;
  background: #f8fafc;
  border: 1px solid #cbd5e1;
  border-radius: 4px;
  cursor: pointer;
}

.additional-info button:hover {
  background: #eef2f7;
}

.additional-info p {
  margin: 12px 0 0;
  color: #475569;
  font-size: 14px;
  line-height: 1.5;
}

.empty-message {
  padding: 24px;
  color: #64748b;
  text-align: center;
}

@media (max-width: 580px) {
  .user-card {
    grid-template-columns: 1fr;
  }

  .user-photo {
    height: 180px;
    min-height: 0;
  }

  .user-content {
    padding: 16px;
  }

  .user-row {
    grid-template-columns: 1fr;
    gap: 2px;
  }
}
</style>
