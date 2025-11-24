<template>
  <div class="app">
    <section class="welcome-section">
      <div class="container position-relative">
        <!-- language selector -->
        <div class="language-selector">
          <button class="lang-btn" @click="toggleDropdown">{{ currentLang.toUpperCase() }}</button>
         
          <div v-if="dropdownOpen" class="lang-dropdown">
            <div class="lang-option" @click="setLanguage('kk')">KZ</div>
            <div class="lang-option" @click="setLanguage('ru')">RU</div>
            <div class="lang-option" @click="setLanguage('en')">EN</div>
          </div>
        </div>



        <div>
    <!-- Корзина иконкасы -->
    <div class="basket" @click="isOpen = true">
      <img src="/images/cart.png" alt="Корзина" />
    </div>

    <!-- Модалды терезе -->
    <Teleport to="body">
      <Transition name="modal">
        <div v-if="isOpen" class="cart-modal" @click="closeBasketModal">
          <div class="cart-content" @click.stop>
            <div class="cart-header">
              <h2>Корзина стола</h2>
              <button class="close-btn" @click="isOpen = false">&times;</button>
            </div>

            <div class="participants">
              <div class="participants-label">Участники:</div>
              <span class="participant-badge">hg</span>
            </div>

            <div class="cart-items">
              <div
                v-for="(item, index) in cartItems"
                :key="index"
                class="cart-item"
              >
                <div class="item-name">{{ item.name }}</div>
                <div class="item-added-by">Добавил: {{ item.addedBy }}</div>
                <div class="quantity-controls">
                  <button @click="decreaseQuantity(index)">−</button>
                  <input type="text" :value="item.quantity" readonly />
                  <button @click="increaseQuantity(index)">+</button>
                </div>
                <div class="price">{{ item.price * item.quantity }} ₽</div>
                <button class="delete-btn" @click="removeItem(index)">🗑️</button>
              </div>
            </div>

            <div class="cart-footer">
              <div class="total">
                <span>Итого:</span>
                <span>{{ total }} ₽</span>
              </div>
              <button class="split-btn">Разделить счёт</button>
              <div class="help-icon">?</div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>

  <div class="lights-container">
          <img src="/images/lightt.png" alt="Light" class="light light-1">
          <img src="/images/lightt.png" alt="Light" class="light light-2">
          <img src="/images/lightt.png" alt="Light" class="light light-3">
        </div> 
  <section class="menu-section">
    <div class="menu-header">
      <h2 class="menu-title">
        <img src="/images/logo.png" alt="Logo" class="menu-logo" id="men">
        Our Menus
      </h2>
      <div class="menu-divider"><hr></div>
    </div>
<div class="menu">
    <div class="menu-content">
      <aside class="menu-sidebar">
        <img src="/images/vertical-menu-bg.png" class="sidebar-bg" alt="bg">

        <nav class="sidebar-nav">
          <ul>
            <li><a class="active" href="#">{{ translations.menuu[currentLang] }}</a></li>
            <li><a href="#">{{ translations.sat[currentLang] }}</a></li>
            <li><a href="#">{{ translations.tan[currentLang] }}</a></li>
            <li><a href="#">{{ translations.sal[currentLang] }}</a></li>
            <li><a href="#">{{ translations.sor[currentLang] }}</a></li>
            <li><a href="#">{{ translations.ult[currentLang] }}</a></li>
            <li><a href="#">{{ translations.sec[currentLang] }}</a></li>
            <li><a href="#">{{ translations.shyg[currentLang] }}</a></li>
            <li><a href="#">{{ translations.det[currentLang] }}</a></li>
            <li><a href="#">{{ translations.lag[currentLang] }}</a></li>
             <li><a href="#">{{ translations.tap[currentLang] }}</a></li>
          </ul>
        </nav>
      </aside>
    </div>

      <div class="menu-content">
      <aside class="menu-sidebar">
        <img src="/images/vertical-menu-bg.png" class="sidebar-bg" alt="bg">

        <nav class="sidebar-nav">
          <ul>
            <li><a class="active" href="#">{{ translations.menuu[currentLang] }}</a></li>
            <li><a href="#">{{ translations.som[currentLang] }}</a></li>
            <li><a href="#">{{ translations.gan[currentLang] }}</a></li>
            <li><a href="#">{{ translations.st[currentLang] }}</a></li>
            <li><a href="#">{{ translations.pas[currentLang] }}</a></li>
            <li><a href="#">{{ translations.nan[currentLang] }}</a></li>
            <li><a href="#">{{ translations.gar[currentLang] }}</a></li>
            <li><a href="#">{{ translations.tuz[currentLang] }}</a></li>
            <li><a href="#">{{ translations.suyk[currentLang] }}</a></li>
              <li><a href="#">{{ translations.bal[currentLang] }}</a></li>
           
          </ul>
        </nav>
      </aside>
    </div>


    <div class="menu-content">
      <aside class="menu-sidebar">
        <img src="/images/vertical-menu-bg.png" class="sidebar-bg" alt="bg">

        <nav class="sidebar-nav">
          <ul>
            <li><a class="active" href="#">{{ translations.bar[currentLang] }}</a></li>
             <li><a href="#">{{ translations.av[currentLang] }}</a></li>
            <li><a href="#">{{ translations.ice[currentLang] }}</a></li>
            <li><a href="#">{{ translations.ys[currentLang] }}</a></li>
            <li><a href="#">{{ translations.des[currentLang] }}</a></li>
            <li><a href="#">{{ translations.cof[currentLang] }}</a></li>
            <li><a href="#">{{ translations.lim[currentLang] }}</a></li>
            <li><a href="#">{{ translations.avv[currentLang] }}</a></li>
            <li><a href="#">{{ translations.mil[currentLang] }}</a></li>
            <li><a href="#">{{ translations.sall[currentLang] }}</a></li>
           
          </ul>
        </nav>
      </aside>
    </div>
    </div>

    <div class="menu-page">

    <!-- Grid -->
    <div class="container">
      <div class="menu-grid">
        <div
          class="menu-card"
          v-for="item in menu"
          :key="item.id"
          @click="openModal(item)"
        >
          <div class="card-text">
            <h3>{{ item.name }}</h3>
            <p class="desc">{{ item.desc }}</p>
            <p class="price">{{ item.price }}</p>
          </div>

          <div class="card-img">
            <img :src="item.img" alt="" />
          </div>
        </div>
      </div>
    </div>

    <!-- MODAL -->
   <div v-if="showModal && activeItem" class="modal-overlay" @click="closeModal">
  <div class="modal-box" @click.stop>
    
    <img :src="activeItem.img" class="modal-img" />

    <div class="modal-content">
      <h2>{{ activeItem.name }}</h2>
      <p class="modal-price">{{ activeItem.price }}</p>
      <p class="modal-desc">{{ activeItem.fullDesc }}</p>

      <!-- Quantity -->
      <div class="qty-row">
        <button @click="qty--" :disabled="qty <= 1">−</button>
        <span>{{ qty }}</span>
        <button @click="qty++">+</button>
      </div>

      <!-- Add btn -->
      <button class="add-btn">
        Add to order — {{ activeItem.singlePrice }} ₸
      </button>
    </div>

    <button class="close-btn" @click="closeModal">×</button>
  </div>
</div>

    </div>
  
  </section>
       
     

        <img src="/images/table-set.png" alt="Table Set" class="table-set img-responsive">
      </div>
    </section>

    <div class="container reservation-popular-container">
      <div class="tm-popular-item-card">
        <div class="tm-popular-item">
          <!-- <img src="/images/telegram-cloud-photo-size-2-5264949883184025439-y.jpg" alt="Popular" class="tm-popular-item-img"> -->
        </div>
      </div>

    </div>
  </div>

 
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { useRouter } from 'vue-router';

type Lang = 'kk' | 'ru' | 'en';
type Mode = 'reserve' | 'join';
type Payment = 'kaspi' | 'halyk';

const router = useRouter();


const currentLang = ref<Lang>('kk');
const dropdownOpen = ref(false);
const mode = ref<Mode>('reserve');


function toggleDropdown() {
  dropdownOpen.value = !dropdownOpen.value;
}
function setLanguage(lang: Lang) {
  currentLang.value = lang;
  dropdownOpen.value = false;
}


const translations = {
  menu: { kk: 'Біздің мәзірлер', ru: 'Наши меню', en: 'Our Menus' },
  cafe: { kk: 'Бахарат', ru: 'Бахарат', en: 'Baharat' },
  description: {
    kk:
      'Baharat шайханасы — бұл жай ғана орын емес. Бұл дәм, дәстүр және мәдениетке деген құрмет. Біз қазақ асханасының құндылығын сақтап, оны заманауи әрі жайлы шайхана форматында ұсынуға тырысамыз — қонақтар да, жергілікті тұрғындар да өз үйіндей сезінсін деп.',
    ru:
      'Чайхана Baharat — это не просто место. Это вкус, традиции и уважение к культуре. Мы бережно сохраняем ценность казахской кухни, переосмысляя её в уютном формате чайханы чтобы и гости, и местные чувствовали себя, как дома.',
    en:
      "Baharat Teahouse is more than just a place. It's about taste, tradition, and respect for culture. We carefully preserve the values of Kazakh cuisine, reimagining it in a cozy teahouse setting so that both guests and locals feel at home."
  },
  details: { kk: 'Менюге өту', ru: 'Перейти к меню', en: 'Go to Menu' },
 menuu: { kk: 'Негізгі мәзір', ru: 'Главное меню', en: 'Main Menu' },
 bar: { kk: 'Бар мәзірі', ru: 'Барное меню', en: 'Bar Menu' },
 sat: { kk: 'Үздік сатылым', ru: 'Лучшие продажи', en: 'Best Sellers' },
 tan: { kk: 'Таңғы ас 12:30-ға дейін', ru: 'Завтрак до 12:30', en: 'Breakfast until 12:30' },
 sal: { kk: 'Салаттар', ru: 'Салаты', en: 'Salads' },
sor: { kk: 'Сорпалар', ru: 'Супы', en: 'Soups' },
  ult: { kk: 'Ұлттық тағамдар', ru: 'Национальные блюда', en: 'National dishes' },
  sec: { kk: 'Екінші тағамдар', ru: 'Вторые блюда', en: 'Main courses' },
shyg: { kk: 'Шығыс асханасы', ru: 'Восточная кухня', en: 'Eastern cuisine' },
tap: { kk: 'Тапсырыспен әзірленетін тағамдар', ru: 'Блюда, приготовленные по заказу', en: 'Dishes prepared to order'},
det: { kk: 'Балалар мәзірі', ru: 'Детское меню', en: 'Childrens menu' },
lag: { kk: 'Лагман', ru: 'Лагман', en: 'Lagman' },
som: { kk: 'Цомян', ru: 'Цомян', en: ' Tsomyan'},
gan: { kk: 'Ган фан', ru: 'Ган фан', en: 'Gan fan'},
bal: { kk: ' Балықтан жасалған тағамдар', ru: ' Блюда из рыбы', en: 'Fish dishes' },
st: { kk: 'Стейктер', ru: 'Стейки', en: 'Steaks' },
pas: { kk: 'Паста', ru: 'Паста', en: 'Pasta'},
nan: { kk: 'Нан тіске басарлары', ru: 'Хлебные закуски ', en: 'Bread appetizers'},
gar: { kk: 'Гарнирлер', ru: 'Гарниры', en: 'Side dishes'},
tuz: { kk: 'Тұздықтар', ru: 'Соусы', en: 'Sauces'},
suyk: { kk: 'Суық тағамдар', ru: 'Холодные блюда', en: 'Cold dishes'},
av:{ kk: 'Авторлық ыстық шайлар', ru: 'Авторские горячие чаи', en: 'Signature hot teas'},
ice:{ kk: 'Суық шай', ru: 'Холодный чай', en: 'Ice tea'},
ys:{ kk: 'Ыстық шайлар', ru: 'Горячие чаи', en: 'Hot teas'},
des:{ kk: 'Десерттер', ru: 'Десерты', en: 'Desserts' },
cof:{ kk: 'Кофе', ru: 'Кофе', en: 'Coffee' },
lim:{ kk: 'Лимонад Мохито', ru: 'Лимонад Мохито', en: 'emonade Mojito'},
avv:{ kk: 'Авторлық лимонадтар', ru: 'Авторские лимонады', en: 'Signature lemonades'},
mil:{ kk: ' Милкшейк ', ru: ' Милкшейк ', en: ' Milkshake '},
sall:{ kk: 'Салқын сусындар', ru: 'Холодные напитки', en: 'Cold drinks'},


};


interface MenuItem {
  id: number;
  name: string;
  desc: string;
  fullDesc: string;
  price: string;
  singlePrice: string;
  img: string;
}

const menu = ref<MenuItem[]>([
  {
  id: 1,
  name: "Қантты бәліш",
  desc: "Балаларға арналған тәтті бәліш. Дәмі жеңіл және тәтті…",
  fullDesc:
    "Балаларға арналған тәтті бәліш. Жұмсақ қамыр мен тәтті крем қосылған, үстіне қант ұнтағы себілген. Тағамыңыздың дәмін арттыру үшін үстіне бал қосыңыз!",
  price: "5,15 ₸ – 7,79 ₸",
  singlePrice: "5,15",
  img: "images/menu-1.jpg"
},
{
  id: 2,
  name: "Сырлы бәліш",
  desc: "Жаңа піскен сыр қосылған нәзік бәліш…",
  fullDesc:
    "Жаңа піскен сыр мен жұмсақ қамырдан жасалған бәліш. Қыздырылған кезде дәмі керемет болады, үстіне жаңа көкөніс қосып, толық тәжірибе алыңыз!",
  price: "6,00 ₸ – 8,50 ₸",
  singlePrice: "6,00",
  img: "images/menu-2.jpg"
},
{
  id: 3,
  name: "Көкөніс салаты",
  desc: "Жаңа көкөністер мен дәмдеуіштерден дайындалған салат…",
  fullDesc:
    "Жаңа піскен көкөністер, зәйтүн майы және дәмдеуіштерден жасалған салат. Жеңіл және пайдалы тағам, түскі немесе кешкі асқа тамаша үйлеседі!",
  price: "4,50 ₸ – 6,00 ₸",
  singlePrice: "4,50",
  img: "images/menu-3.jpg"
},
{
  id: 4,
  name: "Шоколадты торт",
  desc: "Қою шоколад пен кілегейлі крем қосылған тәтті торт…",
  fullDesc:
    "Қою шоколадтан жасалған торт, үстіне крем және жаңғақ қосылған. Мерекелік үстелге немесе тәтті сүйетіндерге арналған керемет десерт!",
  price: "7,00 ₸ – 9,50 ₸",
  singlePrice: "7,00",
  img: "images/popular-2.jpg"
}

]);

const showModal = ref(false);
const activeItem = ref<MenuItem | null>(null);
const qty = ref(1);


function openModal(item: MenuItem) {
  activeItem.value = item;
  qty.value = 1;
  showModal.value = true;
}


function closeModal() {
  showModal.value = false;
  activeItem.value = null;
}




const isOpen = ref(false)

interface CartItem {
  name: string;
  addedBy: string;
  price: number;
  quantity: number;
}

const cartItems = ref<CartItem[]>([
  { name: 'Цезарь с курицей', addedBy: 'hg', price: 650, quantity: 1 },
  { name: 'Том Ям', addedBy: 'hg', price: 550, quantity: 1 }
])


const increaseQuantity = (index: number) => {
  const item = cartItems.value[index]
  if (!item) return
  item.quantity++
}

const decreaseQuantity = (index: number) => {
  const item = cartItems.value[index]
  if (!item) return
  if (item.quantity > 1) item.quantity--
}

const removeItem = (index: number) => {
  if (cartItems.value[index]) {
    cartItems.value.splice(index, 1)
  }
}

const total = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + item.price * item.quantity, 0)
});


const closeBasketModal = () => {
  isOpen.value = false
}
</script>

<style scoped>

html, body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  font-family: 'Arial', sans-serif;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
  position: relative;
}

.language-selector {
  position: absolute;
  top: 10px;
  right: -125px;
  z-index: 30;
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
  margin-top: 8px;
  border-radius: 6px;
  overflow: hidden;
}

.lang-option {
  padding: 8px 12px;
  cursor: pointer;
  color: #fff;
  white-space: nowrap;
}
.lang-option:hover {
  background: #CB9C55;
}


.welcome-section {
  position: relative;
  background-color: #282725;
  color: #fff;
  padding: 40px 0 60px;
  min-height: 720px;
  
}

.lights-container {
  position: absolute;
  left: 38%;
  transform: translateX(-50%);
  display: flex;
  gap: 48px;
  top: -37px; 
  z-index: 1;
}

.welcome-content {
  position: relative;
  text-align: center;
  z-index: 5;
  padding-top: 200px;
}

.welcome-handwriting {
  font-family: 'Pacifico', cursive;
  font-size: 42px;
  color: #fff;
  font-style: italic;
  margin-bottom: 8px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.cafe-title {
  font-family: 'Georgia', serif;
  font-size: 68px;
  color: #CB9C55;
  font-weight: 400;
  margin: 6px 0 12px;
  line-height: 1.05;
}

.cafe-description {
  font-size: 18px;
  color: #d0d0d0;
  margin: 10px auto 22px;
  max-width: 700px;
  text-align: center;
  line-height: 1.6;
}


.more-button {
  display: inline-block;
  padding: 10px 22px;
  background: #CB9C55;
  color: #fff;
  border-radius: 8px;
  text-decoration: none;
  margin-top: 10px;
}
.more-button:hover { background: #9d7b48; }


.table-set {
  display: block;
  margin: 22px auto 0;
  max-width: 100%;
  z-index: 2;
}


.card {
  background: #ffffff;
  border-radius: 24px;
  box-shadow: 0 6px 16px rgba(0,0,0,0.12);
  padding: 26px;
  width: 90%;
  max-width: 560px;
  text-align: center;
  margin-top: 30px;
}


.mode-switch {
  display: flex;
  background: #FFF7EA;
  border-radius: 20px;
  padding: 6px;
  margin-bottom: 18px;
  gap: 6px;
}

.mode-switch button {
  flex: 1;
  padding: 10px 0;
  border: none;
  border-radius: 16px;
  background: transparent;
  color: #CB9C55;
  font-weight: 600;
  cursor: pointer;
  font-size: 15px;
}

.mode-switch button.active {
  background: #CB9C55;
  box-shadow: 0 4px 10px rgba(0,0,0,0.08);
  color: #ffffff;
}



.menu-section {
  width: 100%;
  padding: 60px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.menu-header {
  text-align: center;
  margin-bottom: 40px;
}

.menu-title {
  font-size: 42px;
  font-weight: 700;
  color: #cfa34a;
  font-family: "Brush Script MT", cursive;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
}

.menu-logo {
  width: 30px;
  height: auto;
}

.menu-divider hr {
  margin-top: 10px;
  width: 920px;
  border: none;
  border-top: 2px solid #cfa34a;
}

.menu-content {
  display: flex;
  width: 100%;
  justify-content: center;
}


.menu{
  display: flex;
  gap: 30px
}
.menu-sidebar {
  position: relative;
  width: 280px;
  padding-top: 20px;
}

.sidebar-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 1;
  pointer-events: none;
}

.sidebar-nav {
  position: relative;
  z-index: 2;
}

.sidebar-nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.sidebar-nav li {
  margin-bottom: 8px;
}

.sidebar-nav a {
  display: block;
  padding: 12px 20px;
  font-size: 18px;
  color: #CB9C55;
  text-decoration: none;
  background: transparent;
  transition: 0.3s;
  border-radius: 4px;
}


.sidebar-nav a:hover {
  display: block;
  padding: 12px 20px;
  font-size: 18px;
  color: white;;
  text-decoration: none;
  background:  #CB9C55;;
  transition: 0.3s;
  border-radius: 4px;
}

.sidebar-nav a.active {
  background-color: #cfa34a;
  color: white;
}.menu-page {
  padding: 40px 0;
  font-family: "Georgia", serif;
}

.container {
  width: 90%;
  max-width: 1100px;
  margin: auto;
}

.menu-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 25px;
}

.menu-card {
  display: flex;
  justify-content: space-between;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 18px;
  cursor: pointer;
  background: white;
  transition: 0.2s;
  color: black;
}
.menu-card:hover {
  transform: scale(1.01);
}

.card-text {
  width: 70%;
}
.card-img {
  width: 95px;
  height: 95px;
}
.card-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}



.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.55);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 50;
  text: black;
}

.modal-box {
  background: white;
  width: 700px;
  max-height: 90vh;
  overflow-y: auto;
  border-radius: 12px;
  position: relative;
  animation: popup 0.25s ease-out;
}

@keyframes popup {
  from { transform: scale(0.9); opacity: 0; }
  to   { transform: scale(1); opacity: 1; }
}

.modal-img {
  width: 100%;
  height: 330px;
  object-fit: cover;
  border-radius: 12px 12px 0 0;
}

.modal-content {
  padding: 25px;
  color:black;
}

.modal-price {
  font-weight: 700;
  margin-top: 5px;
color:black;
}

.modal-desc {
  margin-top: 12px;
  line-height: 1.5;
  font-size: 15px;
}


.qty-row {
  display: flex;
  align-items: center;
  gap: 16px;
  margin: 20px 0;
}
.qty-row button {
  width: 35px;
  height: 35px;
  font-size: 20px;
}


.add-btn {
  width: 100%;
  background: #0094ff;
  border: none;
  padding: 14px;
  border-radius: 6px;
  color: white;
  font-weight: 700;
  cursor: pointer;
  margin-top: 10px;
}


.close-btn {
  position: absolute;
  top: 12px;
  right: 14px;
  background: #eaeaea;
  border: none;
  font-size: 22px;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  cursor: pointer;
}





.basket {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  margin-left: 1080px;
  align-items: center;
  justify-content: end;
  cursor: pointer;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}
.basket img {
  width: 30px;
  margin-top: 10px;
  height: auto;
}

.cart-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: flex-end;
  z-index: 1000;
}

.cart-content {
  background: white;
  width: 100%;
  max-width: 400px;
  border-top-left-radius: 16px;
  border-top-right-radius: 16px;
  padding: 20px;
  box-shadow: 0 -4px 20px rgba(0,0,0,0.1);
  max-height: 80vh;
  overflow-y: auto;
}

.cart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
  padding-bottom: 10px;
  border-bottom: 1px solid #eee;
}

.cart-header h2 {
  margin: 0;
  font-size: 18px;
  font-weight: bold;
}

.close-btn {
  font-size: 24px;
  background: none;
  border: none;
  cursor: pointer;
  color: #666;
}

.participants {
  margin-bottom: 20px;
}
.participants-label {
  font-size: 14px;
  color: #555;
  margin-bottom: 8px;
}
.participant-badge {
  display: inline-flex;
  align-items: center;
  background: #f0f0f0;
  border-radius: 20px;
  padding: 5px 12px;
  font-size: 14px;
  margin-right: 8px;
}
.participant-badge::before {
  content: '';
  display: inline-block;
  width: 8px;
  height: 8px;
  background: #ff5757;
  border-radius: 50%;
  margin-right: 6px;
}

.cart-item {
  background: #fafafa;
  border: 1px solid #eee;
  border-radius: 12px;
  padding: 15px;
  margin-bottom: 15px;
  position: relative;
}
.cart-item:hover {
  border-color: #ff9999;
}
.item-name {
  font-weight: bold;
  font-size: 16px;
  margin-bottom: 4px;
}
.item-added-by {
  font-size: 12px;
  color: #777;
  margin-bottom: 10px;
}
.quantity-controls {
  display: flex;
  align-items: center;
  gap: 10px;
  background: white;
  border-radius: 8px;
  padding: 4px 8px;
  margin-right: 10px;
}
.quantity-controls button {
  background: none;
  border: 1px solid #ddd;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  cursor: pointer;
  font-weight: bold;
}
.quantity-controls input {
  width: 24px;
  text-align: center;
  border: none;
  background: transparent;
  font-weight: bold;
}

.delete-btn {
  position: absolute;
  right: 15px;
  bottom: 15px;
  color: #ff5757;
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
}

.cart-footer {
  margin-top: 20px;
  padding-top: 20px;
  border-top: 1px solid #eee;
}
.total {
  display: flex;
  justify-content: space-between;
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 15px;
}
.split-btn {
  width: 100%;
  padding: 12px;
  background: #e0e0e0;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}
.split-btn:hover {
  background: #d0d0d0;
}
.help-icon {
  position: absolute;
  bottom: 10px;
  right: 10px;
  width: 40px;
  height: 40px;
  background: #222;
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  cursor: pointer;
}
.price {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  max-width: 100%;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

@media (max-width: 768px) {
  .menu-grid {
    grid-template-columns: 1fr;
  }
}
/* responsive */
@media (max-width: 768px) {
  .cafe-title { font-size: 56px; }
  .welcome-handwriting { font-size: 36px; margin-top: 120px; }
  .reservation-popular-container { gap: 18px; padding: 24px 0; }
  .card { width: 92%; padding: 20px; }
}

@media (max-width: 480px) {
  .cafe-title { font-size: 42px; }
  .welcome-handwriting { font-size: 30px; margin-top: 100px; }
  .lights-container { gap: 10px; top: 20px; }
  .card { width: 95%; padding: 16px; }
  .table-set { margin-top: 12px; }
}
</style>
