<template>
  <div class="app">
    <section class="welcome-section">
      <div class="container position-relative">
        <div class="language-selector">
          <button class="lang-btn" @click="toggleDropdown">{{ currentLang.toUpperCase() }}</button>
          <div v-if="dropdownOpen" class="lang-dropdown">
            <div class="lang-option" @click="setLanguage('kk')">KZ</div>
            <div class="lang-option" @click="setLanguage('ru')">RU</div>
            <div class="lang-option" @click="setLanguage('en')">EN</div>
          </div>
        </div>

        <div class="lights-container">
          <img src="/images/light-1.png" alt="Light" class="light light-1">
          <img src="/images/light-1.png" alt="Light" class="light light-2">
          <img src="/images/light-1.png" alt="Light" class="light light-3">
        </div> 

        <div class="row welcome-content">
          <h2 class="welcome-handwriting">
            <img src="/images/header-line.png" alt="Line" class="header-line">
            &nbsp;{{ translations.welcome[currentLang] }}&nbsp;&nbsp;
            <img src="/images/header-line.png" alt="Line" class="header-line">
          </h2>

          <h2 class="cafe-title">{{ translations.cafe[currentLang] }}</h2>

          <p class="cafe-description">{{ translations.description[currentLang] }}</p>

          <a href="#reservation" class="more-button">{{ translations.details[currentLang] }}</a>
        </div>

        <img src="/images/table-set-1.png" alt="Table Set" class="table-set img-responsive">
      </div>
    </section>


    <div class="container reservation-popular-container">


      <div class="tm-popular-item-card">
        <div class="tm-popular-item">
          <img src="/images/IMAGE 2025-11-24 15:44:46.jpg" alt="Popular" class="tm-popular-item-img">
        </div>

  
      </div>

      <div id="reservation" class="card card-small">
      <div class="tm-popular-item-description">
          <h3 class="tm-handwriting-font tm-popular-item-title">
            <span class="tm-handwriting-font bigger-first-letter">BAHARAT</span>
          </h3>
          <hr class="tm-popular-item-hr">

          <p>{{ translations.popularDesc[currentLang] }}</p>
        </div>
        <div class="mode-switch">
          <button :class="{ active: mode === 'reserve' }" @click="mode = 'reserve'">
            {{ texts.reserve[currentLang] }}
          </button>
          <button :class="{ active: mode === 'join' }" @click="mode = 'join'">
            {{ texts.join[currentLang] }}
          </button>
        </div>

        <div class="form-fields">
          <input class="medium-input" type="number" v-model="tableNumber" :placeholder="texts.tableNumber[currentLang]" />
          <input class="medium-input" v-model="reserveName" :placeholder="texts.reserveName[currentLang]" />
          <input class="medium-input" v-model="userName" :placeholder="texts.userName[currentLang]" />

          <div v-if="mode === 'reserve'" class="payment">
            <p>{{ texts.paymentMethod[currentLang] }}</p>
            <label><input type="radio" value="kaspi" v-model="payment" /> {{ texts.kaspi[currentLang] }}</label>
            <label><input type="radio" value="halyk" v-model="payment" /> {{ texts.halyk[currentLang] }}</label>
          </div>

          <button class="submit-btn" @click="submitForm">
            {{ mode === 'reserve' ? texts.reserve[currentLang] : texts.join[currentLang] }}
          </button>

          <p v-if="message" class="message">{{ message }}</p>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from "vue-router";

const currentLang = ref('kk');
const dropdownOpen = ref(false);
const mode = ref('reserve');
const tableNumber = ref('');
const reserveName = ref('');
const userName = ref('');
const payment = ref('kaspi');
const message = ref('');

function toggleDropdown() {
  dropdownOpen.value = !dropdownOpen.value;
}
function setLanguage(lang) {
  currentLang.value = lang;
  dropdownOpen.value = false;
}

const translations = {
  welcome: { kk: 'Қош келдіңіз', ru: 'Добро пожаловать', en: 'Welcome To' },
  cafe: { kk: 'Бахарат', ru: 'Бахарат', en: 'Baharat' },
  description: {
    kk: 'Baharat шайханасы — бұл жай ғана орын емес. Бұл дәм, дәстүр және мәдениетке деген құрмет.Біз қазақ асханасының құндылығын сақтап, оны заманауи әрі жайлы шайхана форматында ұсынуға тырысамыз — қонақтар да, жергілікті тұрғындар да өз үйіндей сезінсін деп.',
    ru: 'Чайхана Baharat — это не просто место. Это вкус, традиции и уважение к культуре.Мы бережно сохраняем ценность казахской кухни, переосмысляя её в уютном формате чайханы чтобы и гости, и местные чувствовали себя, как дома.',
    en: "Baharat Teahouse is more than just a place. It's about taste, tradition, and respect for culture. We carefully preserve the values ​​of Kazakh cuisine, reimagining it in a cozy teahouse setting so that both guests and locals feel at home."
  },
  details: { kk: 'Брондау', ru: 'Бронирование', en: 'Reserve' },

  popularDesc: {
    kk: 'Дәмі тіл үйірер шығыс тағамдарынан ләззат алып, жылы атмосфераны сезініңіз.',
    ru: 'Насладитесь вкуснейшими восточными блюдами и теплой атмосферой.',
    en: 'Enjoy delicious oriental dishes and feel the warm, cozy atmosphere.'
  }
};

const texts = {
  reserve: { kk: 'Бронь жасау', ru: 'Забронировать', en: 'Reserve' },
  join: { kk: 'Қосылу', ru: 'Присоединиться', en: 'Join' },
  tableNumber: { kk: 'Стол нөмірі', ru: 'Номер стола', en: 'Table number' },
  reserveName: { kk: 'Бронь атауы', ru: 'Название брони', en: 'Reservation name' },
  userName: { kk: 'Сіздің атыңыз', ru: 'Ваше имя', en: 'Your name' },
  paymentMethod: { kk: 'Төлем әдісі', ru: 'Метод оплаты', en: 'Payment method' },
  kaspi: { kk: 'Каспий', ru: 'Kaspi', en: 'Kaspi' },
  halyk: { kk: 'Халық банк', ru: 'Halyk Bank', en: 'Halyk Bank' },
  fillFields: { kk: 'Барлық өрістерді толтырыңыз!', ru: 'Заполните все поля!', en: 'Please fill in all fields!' },
  booked: { kk: 'Брондалды!', ru: 'Забронировано!', en: 'Reserved!' },
  joined: { kk: 'Столға қосылды!', ru: 'Присоединились!', en: 'Joined!' }
};

const router = useRouter();

const submitForm = () => {
  if (!tableNumber.value || !reserveName.value || !userName.value) {
    message.value = texts.fillFields[currentLang.value];
    return;
  }

  if (mode.value === "reserve") {
    const data = {
      table: tableNumber.value,
      user: userName.value,
      payment: payment.value
    };

    localStorage.setItem(reserveName.value, JSON.stringify(data));

    message.value = texts.booked[currentLang.value];

    setTimeout(() => {
      router.push("/menu");
    }, 1000);

  } else {
    const saved = localStorage.getItem(reserveName.value);

    if (!saved) {
      message.value = "❌ Мұндай брондау жоқ!";
      return;
    }

    const info = JSON.parse(saved);

    if (info.table === tableNumber.value && info.user === userName.value) {
      message.value = "✅ Столға сәтті қосылдыңыз!";

      setTimeout(() => {
        router.push("/menu");
      }, 1000);

    } else {
      message.value = "❌ Дұрыс ақпарат емес!";
      return;
    }
  }
  tableNumber.value = "";
  reserveName.value = "";
  userName.value = "";
  payment.value = "kaspi";
};
</script>


<style>
html, body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  font-family: 'Arial', sans-serif;
}

.container {
  max-width: 100%;
  padding: 0;
  position: relative;
}

.language-selector {
  position: absolute;
  top: 20px;
  right: 20px;
  z-index: 3;
}

.lang-btn {
  background: #CB9C55;
  color: #fff;
  border: none;
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
}

.lang-dropdown {
  background: #282725;
  border: 1px solid #CB9C55;
  margin-top: 5px;
  border-radius: 6px;
  overflow: hidden;
}

.lang-option {
  padding: 6px 12px;
  cursor: pointer;
  color: #fff;
}

.lang-option:hover {
  background: #CB9C55;
}

.welcome-section {
  position: relative;
  background-color: #282725;
  color: #fff;
  padding: 0;
  height: 950px;
}

.lights-container {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 80px;
  z-index: 1;
}

.welcome-content {
  position: relative;
  text-align: center;
  z-index: 2;
  padding-top: 100px;
}

.welcome-handwriting {
  font-family: 'Pacifico', cursive;
  font-size: 50px;
  color: #fff;
  font-style: italic;
  margin-bottom: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.cafe-title {
  font-family: 'Georgia', serif;
  font-size: 80px;
  color: #CB9C55;
  font-weight: normal;
  margin: 0;
  line-height: 1.1;
}

.cafe-description {
  font-size: 18px;
  color: #b0b0b0;
  margin: 15px auto 30px auto;
  max-width: 600px;
  text-align: center;
  line-height: 1.5;
      font-family: "Open Sans", sans-serif;
}

/* More Button */
.more-button {
  display: inline-block;
  padding: 10px 20px;
  background: #CB9C55;
  color: #fff;
  border-radius: 8px;
  text-decoration: none;
  margin-top: 10px;
}

.more-button:hover {
  background: #9d7b48;
}


.table-set {
  display: block;
  margin: 40px auto 0;
  max-width: 100%;
}


.card {
  background: #ffffff;
  border-radius: 24px;
  box-shadow: 0 6px 16px rgba(0,0,0,0.15);
  padding: 30px;
  width: 90%;
  max-width: 600px;
  text-align: center;
margin-top:30px ;

}


.mode-switch {
  display: flex;
  background:  #FFF7EA;
  border-radius: 20px;
  padding: 8px;
  margin-bottom: 24px;
}

.mode-switch button {
  flex: 1;
  padding: 12px 0;
  border: none;
  border-radius: 20px;
  background: transparent;
  color: #CB9C55;
  font-weight: 600;
  cursor: pointer;
  font-size: 16px;
}

.mode-switch button.active {
  background: #CB9C55;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  color: #ffffff;
}


.form-fields {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.medium-input {
  padding: 14px 16px;
  font-size: 16px;
  border-radius: 20px;
  border: 1px solid  #CB9C55;
  background-color: #FFF7EA;
  outline: none;
}

.medium-input:focus {
  border-color: #CB9C55;
  background-color: #CB9C55;
}


.payment {
  text-align: left;
  font-size: 16px;
}

.payment label {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 6px;
  cursor: pointer;
}

.submit-btn {
  width: 100%;
  padding: 14px;
  background: #CB9C55;
  color: #fff;
  border: none;
  border-radius: 24px;
  font-size: 18px;
  cursor: pointer;
}

.submit-btn:hover {
  background:#CB9C55;
}


.message {
  color:#CB9C55;
  font-weight: 600;
  margin-top: 12px;
  font-size: 16px;
}



.reservation-popular-container {
  display: flex;
  justify-content: center;
  margin-top: 50px ;
  flex-wrap: wrap;
  align-items: flex-start; 
  margin-top: 150px;
  gap: 230px;

}


.tm-popular-item-card {

  border-radius: 20px;
  padding: 20px;
  max-width: 300px;
  text-align: center;
}

.tm-popular-item-img {
  width: 500px;
  border-radius: 12px;
  margin-bottom: 10px;

}


.tm-popular-item-hr {
  border: 1px solid #CB9C55;
  margin-bottom: 10px;
}

@media (max-width: 768px) {

  .lights-container {
    top: 40px;
    gap: 10px;
  }

  .welcome-handwriting {
    font-size: 48px;
    margin-top: 160px;
  }

  .cafe-title {
    font-size: 72px;
  }

  .cafe-description {
    font-size: 22px;
    max-width: 85%;
  }

  .tm-popular-item-img {
    max-width: 380px;
  }
  .right-image-1,
  .right-image-2 {
    display: none !important;
  }
  .card {
    width: 70%;
  }
}
@media (max-width: 480px) {
  .light-1,
  .light-3 {
    display: none !important;
  }

  .light-2 {
    display: block !important;
    margin: 0 auto;
    transform: none;
  }

  .lights-container {
    justify-content: center;
    top: 30px;
    gap: 0;
  }
  .welcome-handwriting {
    font-size: 36px;
    margin-top: 140px;
  }

  .cafe-title {
    font-size: 58px;
  }

  .cafe-description {
    font-size: 18px;
    max-width: 90%;
  }

  .tm-popular-item-img {
    max-width: 360px;
    width: 100%;
  }
  .right-image-1,
  .right-image-2 {
    display: none !important;
  }
  .reservation-popular-container {
    flex-direction: column;
    align-items: center;
    gap: 40px;
    margin-top: 60px;
  }

  .card {
    width: 90%;
    padding: 22px;
  }
}

@media (max-width: 320px) {

  .light-1,
  .light-3 {
    display: none !important;
  }

  .light-2 {
    margin: 0 auto;
  }
  .welcome-handwriting {
    font-size: 30px;
    margin-top: 120px;
  }

  .cafe-title {
    font-size: 48px;
  }

  .cafe-description {
    font-size: 16px;
    max-width: 95%;
  }

  .tm-popular-item-img {
    max-width: 280px;
  }
  .right-image-1,
  .right-image-2 {
    display: none !important;
  }

  .reservation-popular-container {
    gap: 30px;
    margin-top: 40px;
  }

  .card {
    width: 95%;
    padding: 18px;
  }

  .submit-btn {
    font-size: 15px;
  }
}


</style>     