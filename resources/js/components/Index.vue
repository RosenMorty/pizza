<template>
  <div class="wrapper">
    <div class="header">
      <div class="container">
        <div class="header__logo">
          <img alt="Pizza logo" src="img/pizza-logo.svg" width="38"/>
          <div>
            <h1>Open kitchen</h1>
            <p>The best or nothing</p>
          </div>
        </div>
        <div class="header__cart">
          <a class="button button--cart" href="/cart.html">
            <span>{{ price }} ₽</span>
            <div class="button__delimiter"></div>
            <svg
                fill="none"
                height="18"
                viewBox="0 0 18 18"
                width="18"
                xmlns="http://www.w3.org/2000/svg"
            >
              <path
                  d="M6.33333 16.3333C7.06971 16.3333 7.66667 15.7364 7.66667 15C7.66667 14.2636 7.06971 13.6667 6.33333 13.6667C5.59695 13.6667 5 14.2636 5 15C5 15.7364 5.59695 16.3333 6.33333 16.3333Z"
                  stroke="white"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="1.8"
              />
              <path
                  d="M14.3333 16.3333C15.0697 16.3333 15.6667 15.7364 15.6667 15C15.6667 14.2636 15.0697 13.6667 14.3333 13.6667C13.597 13.6667 13 14.2636 13 15C13 15.7364 13.597 16.3333 14.3333 16.3333Z"
                  stroke="white"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="1.8"
              />
              <path
                  d="M4.78002 4.99999H16.3334L15.2134 10.5933C15.1524 10.9003 14.9854 11.176 14.7417 11.3722C14.4979 11.5684 14.1929 11.6727 13.88 11.6667H6.83335C6.50781 11.6694 6.1925 11.553 5.94689 11.3393C5.70128 11.1256 5.54233 10.8295 5.50002 10.5067L4.48669 2.82666C4.44466 2.50615 4.28764 2.21182 4.04482 1.99844C3.80201 1.78505 3.48994 1.66715 3.16669 1.66666H1.66669"
                  stroke="white"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="1.8"
              />
            </svg>
            <span>{{ count }}</span>
          </a>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="container">
        <div class="content__top">
          <div class="categories">
            <ul>
              <li class="active">Все</li>
              <li>Мясные</li>
              <li>Вегетарианская</li>
              <li>Гриль</li>
              <li>Острые</li>
              <li>Закрытые</li>
            </ul>
          </div>
          <div class="sort">
            <div class="sort__label">
              <svg
                  fill="none"
                  height="6"
                  viewBox="0 0 10 6"
                  width="10"
                  xmlns="http://www.w3.org/2000/svg"
              >
                <path
                    d="M10 5C10 5.16927 9.93815 5.31576 9.81445 5.43945C9.69075 5.56315 9.54427 5.625 9.375 5.625H0.625C0.455729 5.625 0.309245 5.56315 0.185547 5.43945C0.061849 5.31576 0 5.16927 0 5C0 4.83073 0.061849 4.68424 0.185547 4.56055L4.56055 0.185547C4.68424 0.061849 4.83073 0 5 0C5.16927 0 5.31576 0.061849 5.43945 0.185547L9.81445 4.56055C9.93815 4.68424 10 4.83073 10 5Z"
                    fill="#2C2C2C"
                />
              </svg>
              <b>Сортировка по:</b>
              <span>популярности</span>
            </div>
            <div class="sort__popup">
              <ul>
                <li class="active">популярности</li>
                <li>цене</li>
                <li>алфавиту</li>
              </ul>
            </div>
          </div>
        </div>
        <h2 class="content__title">Пицца</h2>
        <div class="content__items">
          <pizza
              v-for="pizza in pizzas"
              :id="pizza.id"
              :key="pizza.id"
              :image="pizza.image"
              :price="pizza.price"
              :title="pizza.title"
              :ingredients="pizza.ingredients"
              @add-to-cart="addPizzaToCart"
          ></pizza>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Pizza from './Pizza'
import { ref } from 'vue'
import useCart from '../composables/useCart'

export default {
  components: {
    Pizza,
  },

  setup () {
    const { count, price } = useCart()

    const pizzas = ref([
      {
        id: 1,
        title: 'Пицца от шефа',
        price: 689,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/d7bbbc4c74af442e8b9b3ea2faf3c941_292x292.webp',
        ingredients: 'Пастрами из мраморной говядины, сладкий перец, томаты, красный лук, чеснок, соус ткемали, моцарелла, фирменный томатный соус'
      }, 
      {
        id: 2,
        title: 'Гавайская с альфредо',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/0d033c8eb9b24b21828d2fdb7dc3246d_292x292.webp',
        ingredients: 'Фирменный соус альфредо, цыпленок, моцарелла, ананасы'
      }, 
      {
        id: 3,
        title: 'Сырная',
        price: 299,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/d9c609f1422247f2b87b6293eb461ff0_292x292.webp',
        ingredients: 'Моцарелла, сыры чеддер и пармезан, фирменный соус альфредо'
      }, 
      {
        id: 4,
        title: 'Пепперони фреш',
        price: 299,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/27c9bbd0af3a4d1d84a086d9c2f1656d_292x292.webp',
        ingredients: 'Пикантная пепперони, увеличенная порция моцареллы, томаты, фирменный томатный соус'
      },
      {
        id: 5,
        title: 'Двойной цыпленок',
        price: 389,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/ddadb2bd7f2d40459acddbe2f51a2389_292x292.webp',
        ingredients: 'Цыпленок, моцарелла, фирменный соус альфредо'
      },
      {
        id: 6,
        title: 'Чоризо фреш',
        price: 299,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/02ca2561953b488993878d1f70e359de_292x292.webp',
        ingredients: 'Фирменный томатный соус, моцарелла, острая чоризо, сладкий перец'
      },
      {
        id: 7,
        title: 'Ветчина и сыр',
        price: 389,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/cea570842b754c52b786c231c65bd2e2_292x292.webp',
        ingredients: 'Ветчина, моцарелла, фирменный соус альфредо'
      },
      {
        id: 8,
        title: 'Карбонара',
        price: 539,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/9f54fa5d2d204f5fa70579e2e1982d03_292x292.webp',
        ingredients: 'Бекон, сыры чеддер и пармезан, моцарелла, томаты, красный лук, чеснок, фирменный соус альфредо, итальянские травы'
      },
      {
        id: 9,
        title: 'Деревенская с бужениной',
        price: 489,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/200ef6ddfb814852ad1a2456c5d7c62c_292x292.webp',
        ingredients: 'Запеченная буженина из свинины, моцарелла, картофель из печи, маринованные огурчики, красный лук, чеснок, фирменный томатный соус, соус ранч'
      },
      {
        id: 10,
        title: 'Сырный цыпленок',
        price: 489,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/42360a7dcb7640c998b723231586fe84_292x292.webp',
        ingredients: 'Цыпленок, моцарелла, сыры чеддер и пармезан, сырный соус, томаты, фирменный соус альфредо, чеснок'
      },
      {
        id: 11,
        title: 'Бургер пицца',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/3a948b9d5af14d219e2c54282229755a_292x292.webp',
        ingredients: 'Ветчина, маринованные огурчики, томаты, красный лук, чеснок, соус бургер, моцарелла, фирменный томатный соус'
      },
      {
        id: 12,
        title: 'Песто',
        price: 489,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/ba58ba9c2a3a4dbda7eb618882d7128d_292x292.webp',
        ingredients: 'Цыпленок, соус песто, кубики брынзы, томаты, моцарелла, фирменный соус альфредо'
      },
      {
        id: 13,
        title: 'Мясная',
        price: 489,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/18dbb12240b041a191c9dc73c9c1f4ef_292x292.webp',
        ingredients: 'Цыпленок, ветчина, пикантная пепперони, острая чоризо, моцарелла, фирменный томатный соус'
      },
      {
        id: 14,
        title: 'Цыпленок карри',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/c8ac7d2eb95b4bd0b8bc2f366415896c_292x292.webp',
        ingredients: 'Цыпленок, ананасы, соус карри, красный лук, сладкий перец, моцарелла, фирменный томатный соус'
      },
      {
        id: 15,
        title: 'Доума',
        price: 539,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/2676fc1086464a26801a852a702f5d78_292x292.webp',
        ingredients: 'Бекон, митболы, пикантная пепперони, моцарелла, томаты, шампиньоны, сладкий перец, красный лук, чеснок, фирменный томатный соус'
      },
      {
        id: 16,
        title: 'Цыпленок барбекю',
        price: 539,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/45cc8ffb190c4a28aaf1863a67f675c7_292x292.webp',
        ingredients: 'Цыпленок, бекон, соус барбекю, красный лук, моцарелла, фирменный томатный соус'
      },
      {
        id: 17,
        title: 'Аррива!',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/5907951b8bf848b2b3bf0ead39b84ab1_292x292.webp',
        ingredients: 'Острая чоризо, цыпленок, томаты, соус бургер, сладкий перец, красный лук, моцарелла, соус ранч, чеснок'
      },
      {
        id: 18,
        title: 'Четыре сыра',
        price: 489,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/50555f951a6d4fd4ac0088c099eb3769_292x292.webp',
        ingredients: 'Сыр блю чиз, смесь сыров чеддер и пармезан, моцарелла, фирменный соус альфредо'
      },
      {
        id: 19,
        title: 'Пепперони',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/fb9cc5b8ff2e47bdbcbdcb5930cddf06_292x292.webp',
        ingredients: 'Пикантная пепперони, увеличенная порция моцареллы, фирменный томатный соус'
      },
      {
        id: 20,
        title: 'Цыпленок ранч',
        price: 539,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/e379c72af6c54f81b7b4e6ffbb2b1729_292x292.webp',
        ingredients: 'Цыпленок, ветчина, соус ранч, моцарелла, томаты, чеснок'
      },
      {
        id: 21,
        title: 'Ветчина грибы',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/0c24c7c195574d7cae45c889bd8043fc_292x292.webp',
        ingredients: 'Ветчина, шампиньоны, увеличенная порция моцареллы, фирменный томатный соус'
      },
      {
        id: 22,
        title: 'Домашняя',
        price: 389,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/1737ebbfb03148a291f8b3060cd9f0a1_292x292.webp',
        ingredients: 'Пикантная пепперони, ветчина, маринованные огурчики, томаты, моцарелла, фирменный томатный соус'
      },
      {
        id: 23,
        title: 'Диабло',
        price: 539,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/03c840b1ab6f4ccb84f5dc167e146598_292x292.webp',
        ingredients: 'Острая чоризо, острый перец халапеньо, соус барбекю, митболы, томаты, сладкий перец, красный лук, моцарелла, фирменный томатный соус'
      },
      {
        id: 24,
        title: 'Маргарита',
        price: 389,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/748949429e25404ea10aab002c910d84_292x292.webp',
        ingredients: 'Увеличенная порция моцареллы, томаты, итальянские травы, фирменный томатный соус'
      },
      {
        id: 25,
        title: 'Колбаски барбекю',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/10b95b8611ec457dbffd9613b8eb165a_292x292.webp',
        ingredients: 'Острая чоризо, соус барбекю, томаты, красный лук, моцарелла, фирменный томатный соус'
      },
      {
        id: 26,
        title: 'Овощи и грибы',
        price: 439,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/d6c9f93ea37649ac923e9586c034a5a0_292x292.webp',
        ingredients: 'Шампиньоны, томаты, сладкий перец, красный лук, кубики брынзы, моцарелла, фирменный томатный соус, итальянские травы'
      },
      {
        id: 27,
        title: 'Двойная пепперони',
        price: 489,
        image: 'https://dodopizza-a.akamaihd.net/static/Img/Products/b8880e1ce9b84e78aa3004d5b86d5bf9_292x292.webp',
        ingredients: 'Двойная порция пикантной пепперони, увеличенная порция моцареллы, фирменный томатный соус'
      },
    ])

    return {
      pizzas,
      count,
      price
    }
  }
}
</script>