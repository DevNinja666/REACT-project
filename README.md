# REACT-project
================================================================================
                    ДОКУМЕНТАЦИЯ ПРОЕКТА ECOMMERCE SHOP
================================================================================

ОБЩЕЕ ОПИСАНИЕ ПРОЕКТА
================================================================================

Название: Ecommerce Shop
Тип: Single Page Application (SPA) интернет-магазин
Технологии: React 18, TypeScript, Redux Toolkit, React Router, Tailwind CSS
Сборщик: Vite
Стилизация: Tailwind CSS с кастомными шрифтами (Inter, Poppins)
Хранение данных: localStorage (без backend)

Проект представляет собой полнофункциональный интернет-магазин с возможностью:
- Регистрации и авторизации пользователей
- Просмотра каталога товаров
- Добавления товаров в корзину и избранное
- Добавления и редактирования товаров (для авторизованных пользователей)
- Управления корзиной покупок

СТРУКТУРА ПРОЕКТА
================================================================================

ecommerce-shop/
├── index.html                    # Главный HTML файл
├── package.json                  # Зависимости и скрипты проекта
├── package-lock.json             # Зафиксированные версии зависимостей
├── vite.config.ts               # Конфигурация Vite
├── tsconfig.json                 # Конфигурация TypeScript
├── tsconfig.node.json            # Конфигурация TypeScript для Node
├── tailwind.config.js            # Конфигурация Tailwind CSS
├── postcss.config.js             # Конфигурация PostCSS
├── README.md                     # Краткое описание проекта
└── src/                          # Исходный код приложения
    ├── main.tsx                  # Точка входа приложения
    ├── App.tsx                   # Главный компонент с роутингом
    ├── index.css                 # Глобальные стили
    ├── types/                    # TypeScript типы
    │   └── index.ts
    ├── store/                    # Redux хранилище
    │   ├── store.ts
    │   ├── hooks.ts
    │   ├── authSlice.ts
    │   ├── productsSlice.ts
    │   ├── cartSlice.ts
    │   └── favoritesSlice.ts
    ├── components/               # Переиспользуемые компоненты
    │   ├── Layout/
    │   │   └── Layout.tsx
    │   ├── ProductCard/
    │   │   └── ProductCard.tsx
    │   ├── Cart/
    │   │   └── Cart.tsx
    │   ├── CartItem/
    │   │   └── CartItem.tsx
    │   └── FavoriteItem/
    │       └── FavoriteItem.tsx
    └── pages/                    # Страницы приложения
        ├── Home/
        │   └── Home.tsx
        ├── CartPage/
        │   └── CartPage.tsx
        ├── FavoritesPage/
        │   └── FavoritesPage.tsx
        ├── LoginPage/
        │   └── LoginPage.tsx
        ├── RegisterPage/
        │   └── RegisterPage.tsx
        ├── AddProductPage/
        │   └── AddProductPage.tsx
        └── EditProductPage/
            └── EditProductPage.tsx

ПОДРОБНОЕ ОПИСАНИЕ ФАЙЛОВ
================================================================================

КОНФИГУРАЦИОННЫЕ ФАЙЛЫ
================================================================================

1. package.json
   Описание: Определяет зависимости проекта и npm скрипты
   Содержимое:
   - name: "ecommerce-shop"
   - version: "1.0.0"
   - type: "module" (ES модули)
   - scripts:
     * dev: запуск dev сервера Vite
     * build: сборка проекта (TypeScript компиляция + Vite build)
     * preview: предпросмотр собранного проекта
   - dependencies:
     * @reduxjs/toolkit: ^2.11.2 (управление состоянием)
     * react: ^18.2.0
     * react-dom: ^18.2.0
     * react-redux: ^9.2.0 (интеграция Redux с React)
     * react-router-dom: ^7.11.0 (маршрутизация)
   - devDependencies:
     * TypeScript и типы
     * Vite и плагины
     * Tailwind CSS и PostCSS
     * Autoprefixer

2. vite.config.ts
   Описание: Конфигурация сборщика Vite
   Содержимое:
   - plugins: [react()] - плагин для поддержки React
   - Использует стандартную конфигурацию Vite

3. tsconfig.json
   Описание: Конфигурация TypeScript компилятора
   Содержимое:
   - target: ES2020
   - module: ESNext
   - jsx: "react-jsx"
   - strict: true (строгая проверка типов)
   - Настройки для современного React и TypeScript

4. tailwind.config.js
   Описание: Конфигурация Tailwind CSS
   Содержимое:
   - content: пути к файлам для сканирования классов
   - theme: расширение темы (по умолчанию)
   - plugins: пустой массив

5. postcss.config.js
   Описание: Конфигурация PostCSS
   Содержимое:
   - plugins: tailwindcss и autoprefixer

6. index.html
   Описание: Главный HTML файл приложения
   Содержимое:
   - Подключение Google Fonts (Inter, Poppins)
   - div#root для монтирования React приложения
   - Подключение main.tsx как модуля

ОСНОВНЫЕ ФАЙЛЫ ПРИЛОЖЕНИЯ
================================================================================

7. src/main.tsx
   Описание: Точка входа приложения
   Содержимое:
   - Импорт React и ReactDOM
   - Импорт Redux Provider и store
   - Импорт главного компонента App
   - Импорт глобальных стилей
   - Создание root элемента
   - Оборачивание приложения в:
     * React.StrictMode (режим строгой проверки)
     * Provider store={store} (Redux провайдер)
   - Монтирование App компонента

8. src/App.tsx
   Описание: Главный компонент с настройкой роутинга
   Содержимое:
   - Импорт BrowserRouter, Routes, Route, Navigate из react-router-dom
   - Импорт всех страниц приложения
   - Импорт Layout компонента
   - Импорт useAppSelector для проверки авторизации
   - ProtectedRoute компонент:
     * Проверяет isAuthenticated из Redux store
     * Если не авторизован - редирект на /login
     * Если авторизован - рендерит children
   - Маршруты:
     * / - Home (главная страница)
     * /cart - CartPage (корзина)
     * /favorites - FavoritesPage (избранное)
     * /login - LoginPage (вход)
     * /register - RegisterPage (регистрация)
     * /add-product - AddProductPage (защищенный, только для авторизованных)
     * /edit/:id - EditProductPage (защищенный, только для владельца товара)
   - Все маршруты обернуты в Layout компонент

9. src/index.css
   Описание: Глобальные стили приложения
   Содержимое:
   - @tailwind base, components, utilities (директивы Tailwind)
   - Стили для html и body:
     * margin: 0, padding: 0
     * height: 100%
     * overflow-x: hidden (скрытие горизонтального скролла)
     * overflow-y: auto (вертикальный скролл только при необходимости)
     * font-family: Inter, Poppins и системные шрифты
     * -webkit-font-smoothing и -moz-osx-font-smoothing для сглаживания
   - #root: min-height: 100vh, flex layout
   - *: font-family: 'Inter'
   - h1-h6: font-family: 'Poppins', font-weight: 600

ТИПЫ (src/types/index.ts)
================================================================================

10. src/types/index.ts
    Описание: TypeScript интерфейсы для типизации данных
    Содержимое:
    - interface User:
      * id: string (уникальный идентификатор)
      * name: string (имя пользователя)
      * email: string (email пользователя)
    - interface Product:
      * id: string (уникальный идентификатор товара)
      * title: string (название товара)
      * price: number (цена товара)
      * image: string (URL изображения)
      * ownerId: string (ID пользователя-владельца)
    - interface CartItem:
      * product: Product (объект товара)
      * quantity: number (количество товара)

REDUX STORE (src/store/)
================================================================================

11. src/store/store.ts
    Описание: Главный файл Redux store
    Содержимое:
    - Импорт configureStore из @reduxjs/toolkit
    - Импорт всех reducers (auth, products, cart, favorites)
    - Создание store с помощью configureStore:
      * reducer: объект с всеми слайсами
    - Экспорт типов:
      * RootState: тип всего состояния store
      * AppDispatch: тип dispatch функции

12. src/store/hooks.ts
    Описание: Типизированные хуки для работы с Redux
    Содержимое:
    - useAppDispatch: типизированная версия useDispatch
    - useAppSelector: типизированная версия useSelector
    - Используются для type-safe работы с Redux в компонентах

13. src/store/authSlice.ts
    Описание: Redux slice для управления авторизацией
    Содержимое:
    - interface AuthState:
      * currentUser: User | null (текущий пользователь)
      * isAuthenticated: boolean (статус авторизации)
    - loadAuthFromStorage(): загружает данные из localStorage
    - initialState: загружается из localStorage при инициализации
    - Reducers:
      * login: устанавливает пользователя и isAuthenticated = true, сохраняет в localStorage
      * logout: очищает пользователя и isAuthenticated = false, удаляет из localStorage
      * register: аналогично login (автоматический вход после регистрации)
    - Экспорт actions: login, logout, register

14. src/store/productsSlice.ts
    Описание: Redux slice для управления товарами
    Содержимое:
    - interface ProductsState:
      * products: Product[] (массив всех товаров)
    - loadProductsFromStorage(): загружает товары из localStorage
    - initialState: загружается из localStorage
    - Reducers:
      * addProduct: добавляет новый товар в массив, сохраняет в localStorage
      * updateProduct: находит товар по ID и обновляет его, сохраняет в localStorage
      * deleteProduct: удаляет товар по ID, сохраняет в localStorage
    - Экспорт actions: addProduct, updateProduct, deleteProduct

15. src/store/cartSlice.ts
    Описание: Redux slice для управления корзиной покупок
    Содержимое:
    - interface CartState:
      * items: CartItem[] (массив товаров в корзине)
    - loadCartFromStorage(): загружает корзину из localStorage
    - initialState: загружается из localStorage
    - Reducers:
      * addToCart: 
        - Проверяет, есть ли товар уже в корзине
        - Если есть - увеличивает quantity на 1
        - Если нет - добавляет новый CartItem с quantity = 1
        - Сохраняет в localStorage
      * removeFromCart: удаляет товар по ID, сохраняет в localStorage
      * updateQuantity:
        - Находит товар по ID
        - Если quantity <= 0 - удаляет товар
        - Иначе обновляет quantity
        - Сохраняет в localStorage
      * clearCart: очищает корзину, удаляет из localStorage
    - Экспорт actions: addToCart, removeFromCart, updateQuantity, clearCart

16. src/store/favoritesSlice.ts
    Описание: Redux slice для управления избранными товарами
    Содержимое:
    - interface FavoritesState:
      * products: Product[] (массив избранных товаров)
    - loadFavoritesFromStorage(): загружает избранное из localStorage
    - initialState: загружается из localStorage
    - Reducers:
      * addToFavorites:
        - Проверяет, есть ли товар уже в избранном
        - Если нет - добавляет товар
        - Сохраняет в localStorage
      * removeFromFavorites: удаляет товар по ID, сохраняет в localStorage
    - Экспорт actions: addToFavorites, removeFromFavorites

КОМПОНЕНТЫ (src/components/)
================================================================================

17. src/components/Layout/Layout.tsx
    Описание: Компонент макета с навигационной панелью
    Содержимое:
    - Props: children (React.ReactNode)
    - Использует useAppDispatch и useAppSelector для работы с Redux
    - Использует useNavigate для программной навигации
    - Получает из store:
      * isAuthenticated, currentUser (из auth)
      * cartItems (из cart) для подсчета количества
    - Функции:
      * handleLogout: вызывает logout action и перенаправляет на главную
    - Структура:
      * Внешний div с bg-gray-50 и flex layout
      * Navbar (nav):
        - bg-blue-600 (синий фон)
        - rounded-2xl (скругленные углы)
        - Адаптивные отступы
        - Содержит:
          * Логотип "Ecommerce Shop" (ссылка на /)
          * Навигационные ссылки: Home, Favorites, Add Product (если авторизован)
          * Иконка корзины с бейджем количества
          * Если авторизован: приветствие и кнопка Logout
          * Если не авторизован: кнопки Login и Register
      * Main контейнер с children (контент страниц)
    - Адаптивный дизайн: flex-col на мобильных, flex-row на десктопе

18. src/components/ProductCard/ProductCard.tsx
    Описание: Компонент карточки товара
    Содержимое:
    - Props: product (Product)
    - Использует useNavigate, useAppDispatch, useAppSelector
    - Получает из store:
      * currentUser, isAuthenticated (из auth)
      * favorites (из favorites) для проверки, является ли товар избранным
    - Вычисляет:
      * isFavorite: проверяет, есть ли товар в избранном
      * canEdit: проверяет, может ли пользователь редактировать товар
        (авторизован И ownerId === currentUser.id)
    - Функции:
      * handleAddToCart: добавляет товар в корзину
      * handleToggleFavorite: переключает статус избранного
      * handleEdit: перенаправляет на страницу редактирования
    - Структура:
      * Карточка с bg-gray-50, rounded-xl, shadow
      * Изображение товара (h-48 sm:h-56 md:h-64)
      * Кнопка избранного (сердце) в правом верхнем углу
      * Название товара
      * Цена (синий цвет)
      * Кнопка "Add to Cart"
      * Кнопка "Edit" (только если canEdit === true)
    - Адаптивный дизайн

19. src/components/Cart/Cart.tsx
    Описание: Компонент корзины покупок
    Содержимое:
    - Использует useAppSelector для получения cartItems
    - Вычисляет total: сумма всех товаров (price * quantity)
    - Если корзина пуста:
      * Показывает сообщение "Your cart is empty"
      * Кнопка "Continue Shopping" (ссылка на /)
    - Если корзина не пуста:
      * Заголовок "Shopping Cart"
      * Список CartItem компонентов
      * Блок с итоговой суммой (bg-gray-50)
      * Кнопка "Checkout"
    - Адаптивный дизайн

20. src/components/CartItem/CartItem.tsx
    Описание: Компонент элемента корзины
    Содержимое:
    - Props: item (CartItem)
    - Использует useAppDispatch
    - Функции:
      * handleQuantityChange: обновляет количество товара
      * handleRemove: удаляет товар из корзины
    - Структура:
      * Изображение товара (адаптивное)
      * Название и цена товара
      * Кнопки управления количеством (- и +)
      * Отображение текущего количества
      * Итоговая цена (price * quantity)
      * Кнопка "Remove"
    - Адаптивный дизайн: flex-col на мобильных, flex-row на десктопе

21. src/components/FavoriteItem/FavoriteItem.tsx
    Описание: Компонент элемента избранного
    Содержимое:
    - Props: product (Product)
    - Использует useAppDispatch
    - Функции:
      * handleRemove: удаляет товар из избранного
      * handleAddToCart: добавляет товар в корзину
    - Структура:
      * Изображение товара
      * Название и цена товара
      * Кнопка "Add to Cart"
      * Кнопка "Remove"
    - Адаптивный дизайн

СТРАНИЦЫ (src/pages/)
================================================================================

22. src/pages/Home/Home.tsx
    Описание: Главная страница с каталогом товаров
    Содержимое:
    - Использует useAppSelector для получения products
    - Если товаров нет:
      * Показывает сообщение "No products available yet."
    - Если товары есть:
      * Заголовок "Product Catalog"
      * Сетка товаров (grid):
        - 1 колонка на мобильных
        - 2 колонки на планшетах (md)
        - 3 колонки на больших экранах (lg)
        - 4 колонки на очень больших экранах (xl)
      * Каждый товар отображается через ProductCard компонент
    - Адаптивный дизайн

23. src/pages/CartPage/CartPage.tsx
    Описание: Страница корзины покупок
    Содержимое:
    - Простой wrapper компонент
    - Оборачивает Cart компонент в контейнер с адаптивными отступами
    - Использует контейнер с адаптивными padding

24. src/pages/FavoritesPage/FavoritesPage.tsx
    Описание: Страница избранных товаров
    Содержимое:
    - Использует useAppSelector для получения favorites
    - Если избранное пусто:
      * Показывает сообщение "Your favorites list is empty."
      * Подсказка "Add products to favorites to see them here."
    - Если избранное не пусто:
      * Заголовок "Favorites"
      * Список FavoriteItem компонентов
    - Адаптивный дизайн

25. src/pages/LoginPage/LoginPage.tsx
    Описание: Страница входа в систему
    Содержимое:
    - Использует useState для:
      * email, password (поля формы)
      * error (сообщения об ошибках)
    - Использует useNavigate и useAppDispatch
    - Функция handleSubmit:
      * Проверяет наличие пользователей в localStorage
      * Ищет пользователя по email
      * Проверяет пароль из userData в localStorage
      * При успехе: вызывает login action и перенаправляет на /
      * При ошибке: показывает сообщение об ошибке
    - Структура:
      * Центрированная форма
      * Поля: Email, Password
      * Кнопка "Login"
      * Ссылка на страницу регистрации
      * Отображение ошибок (если есть)
    - Адаптивный дизайн
    - bg-gray-50 фон

26. src/pages/RegisterPage/RegisterPage.tsx
    Описание: Страница регистрации
    Содержимое:
    - Использует useState для:
      * name, email, password, confirmPassword
      * error
    - Использует useNavigate и useAppDispatch
    - Функция handleSubmit:
      * Проверяет совпадение паролей
      * Проверяет длину пароля (минимум 6 символов)
      * Проверяет, не существует ли уже пользователь с таким email
      * Создает нового пользователя с уникальным ID (Date.now())
      * Сохраняет пользователя в localStorage (ключ "users")
      * Сохраняет пароль в localStorage (ключ "userData", email -> password)
      * Вызывает register action (автоматический вход)
      * Перенаправляет на /
    - Структура:
      * Центрированная форма
      * Поля: Name, Email, Password, Confirm Password
      * Кнопка "Register"
      * Ссылка на страницу входа
      * Отображение ошибок
    - Адаптивный дизайн
    - bg-gray-50 фон

27. src/pages/AddProductPage/AddProductPage.tsx
    Описание: Страница добавления нового товара (защищенная)
    Содержимое:
    - Использует useState для: title, price, image
    - Использует useNavigate, useAppDispatch, useAppSelector
    - useEffect:
      * Проверяет авторизацию
      * Если не авторизован - перенаправляет на /login
    - Функция handleSubmit:
      * Создает новый Product с:
        - id: Date.now().toString()
        - title, price (parseFloat), image
        - ownerId: currentUser.id
      * Вызывает addProduct action
      * Перенаправляет на /
    - Если не авторизован - возвращает null
    - Структура:
      * Центрированная форма
      * Поля: Title, Price (number), Image URL
      * Кнопки: "Add Product" и "Cancel"
    - Адаптивный дизайн
    - bg-gray-50 фон

28. src/pages/EditProductPage/EditProductPage.tsx
    Описание: Страница редактирования товара (защищенная)
    Содержимое:
    - Использует useParams для получения id из URL
    - Использует useState для: title, price, image
    - Использует useNavigate, useAppDispatch, useAppSelector
    - Получает product из store по id
    - useEffect:
      * Проверяет авторизацию - редирект на /login
      * Проверяет существование товара - редирект на /
      * Проверяет владельца (product.ownerId === currentUser.id) - редирект на /
      * Заполняет форму данными товара
    - Функция handleSubmit:
      * Создает обновленный Product
      * Вызывает updateProduct action
      * Перенаправляет на /
    - Если не авторизован или не владелец - возвращает null
    - Структура:
      * Центрированная форма
      * Поля: Title, Price, Image URL (заполнены текущими данными)
      * Кнопки: "Save Changes" и "Cancel"
    - Адаптивный дизайн
    - bg-gray-50 фон

ЛОГИКА РАБОТЫ ПРИЛОЖЕНИЯ
================================================================================

АВТОРИЗАЦИЯ
--------------------------------------------------------------------------------
1. Регистрация:
   - Пользователь заполняет форму (имя, email, пароль, подтверждение)
   - Данные сохраняются в localStorage:
     * "users": массив объектов User
     * "userData": объект {email: password}
   - После регистрации автоматически вызывается register action
   - Пользователь считается авторизованным
   - Состояние сохраняется в localStorage ("auth")

2. Вход:
   - Пользователь вводит email и пароль
   - Проверка через localStorage:
     * Поиск пользователя в "users" по email
     * Проверка пароля в "userData"
   - При успехе вызывается login action
   - Состояние сохраняется в localStorage

3. Выход:
   - Вызывается logout action
   - Очищается состояние и localStorage

УПРАВЛЕНИЕ ТОВАРАМИ
--------------------------------------------------------------------------------
1. Добавление товара:
   - Доступно только авторизованным пользователям
   - Товар создается с ownerId = currentUser.id
   - Сохраняется в Redux store и localStorage

2. Редактирование товара:
   - Доступно только владельцу товара
   - Проверка: product.ownerId === currentUser.id
   - Обновление через updateProduct action

3. Просмотр товаров:
   - Все товары видны всем пользователям
   - Неавторизованные могут просматривать, добавлять в корзину/избранное

КОРЗИНА ПОКУПОК
--------------------------------------------------------------------------------
1. Добавление в корзину:
   - Если товар уже в корзине - увеличивается quantity
   - Если товара нет - добавляется с quantity = 1
   - Сохраняется в localStorage

2. Управление количеством:
   - Кнопки + и - для изменения quantity
   - Если quantity = 0 - товар удаляется
   - Сохраняется в localStorage

3. Удаление:
   - Кнопка "Remove" удаляет товар из корзины
   - Сохраняется в localStorage

ИЗБРАННОЕ
--------------------------------------------------------------------------------
1. Добавление в избранное:
   - Проверка на дубликаты (по id)
   - Если товара нет - добавляется
   - Сохраняется в localStorage

2. Удаление из избранного:
   - Удаление по id
   - Сохраняется в localStorage

3. Переключение:
   - Кнопка-сердце на карточке товара
   - Красное = в избранном, белое = не в избранном

ХРАНЕНИЕ ДАННЫХ
================================================================================

Все данные хранятся в localStorage браузера:

1. "auth" - объект с текущей сессией:
   {
     currentUser: {id, name, email},
     isAuthenticated: true/false
   }

2. "users" - массив всех зарегистрированных пользователей:
   [
     {id, name, email},
     ...
   ]

3. "userData" - объект для проверки паролей:
   {
     "email1": "password1",
     "email2": "password2",
     ...
   }

4. "products" - массив всех товаров:
   [
     {id, title, price, image, ownerId},
     ...
   ]

5. "cart" - массив товаров в корзине:
   [
     {product: {...}, quantity: 2},
     ...
   ]

6. "favorites" - массив избранных товаров:
   [
     {id, title, price, image, ownerId},
     ...
   ]

При загрузке приложения все данные восстанавливаются из localStorage.

МАРШРУТИЗАЦИЯ
================================================================================

Маршруты определены в App.tsx:

1. / - Home (публичный)
2. /cart - CartPage (публичный)
3. /favorites - FavoritesPage (публичный)
4. /login - LoginPage (публичный)
5. /register - RegisterPage (публичный)
6. /add-product - AddProductPage (защищенный, требует авторизации)
7. /edit/:id - EditProductPage (защищенный, требует авторизации и владения)

Защищенные маршруты используют ProtectedRoute компонент, который:
- Проверяет isAuthenticated из Redux store
- Если не авторизован - редирект на /login
- Если авторизован - рендерит содержимое

СТИЛИЗАЦИЯ
================================================================================

1. Tailwind CSS:
   - Utility-first подход
   - Адаптивные классы (sm:, md:, lg:, xl:)
   - Кастомные цвета: blue-600 (основной), gray-50 (фон)

2. Шрифты:
   - Inter - для основного текста
   - Poppins - для заголовков (h1-h6)
   - Подключены через Google Fonts

3. Цветовая схема:
   - Основной цвет: синий (blue-600 для navbar, blue-500 для кнопок)
   - Фон: светло-серый (gray-50)
   - Цены: синий (blue-600)
   - Текст: серый (gray-700, gray-800)

4. Адаптивность:
   - Мобильные: 1 колонка, вертикальная навигация
   - Планшеты: 2 колонки
   - Десктоп: 3-4 колонки, горизонтальная навигация

ОСОБЕННОСТИ РЕАЛИЗАЦИИ
================================================================================

1. TypeScript:
   - Строгая типизация всех данных
   - Интерфейсы для User, Product, CartItem
   - Типизированные Redux хуки

2. Redux Toolkit:
   - Использование createSlice для создания reducers
   - Автоматическая генерация actions
   - Immer для иммутабельных обновлений

3. React Router:
   - BrowserRouter для HTML5 истории
   - Защищенные маршруты через компонент
   - Динамические параметры (:id)

4. localStorage:
   - Синхронизация с Redux store
   - Загрузка при инициализации
   - Сохранение при каждом изменении

5. Адаптивный дизайн:
   - Mobile-first подход
   - Breakpoints: sm (640px), md (768px), lg (1024px), xl (1280px)
   - Гибкие сетки и flexbox

6. UX особенности:
   - Визуальная обратная связь (hover эффекты)
   - Плавные переходы (transition)
   - Индикаторы (бейджи, иконки)
   - Сообщения об ошибках
   - Пустые состояния

ЗАПУСК ПРОЕКТА
================================================================================

1. Установка зависимостей:
   npm install

2. Запуск dev сервера:
   npm run dev

3. Сборка для продакшена:
   npm run build

4. Просмотр собранной версии:
   npm run preview

ТРЕБОВАНИЯ
================================================================================

- Node.js (версия 16+)
- npm или yarn
- Современный браузер с поддержкой ES6+

ЗАВИСИМОСТИ
================================================================================

Основные:
- React 18.2.0
- React DOM 18.2.0
- Redux Toolkit 2.11.2
- React Redux 9.2.0
- React Router DOM 7.11.0

Разработка:
- TypeScript 5.2.2
- Vite 5.0.8
- Tailwind CSS 3.3.6
- PostCSS 8.4.32
- Autoprefixer 10.4.16

СТРУКТУРА КОМПОНЕНТОВ
================================================================================

Все компоненты используют функциональный подход с хуками:
- useState для локального состояния
- useEffect для побочных эффектов
- useAppDispatch для dispatch actions
- useAppSelector для получения данных из store
- useNavigate для программной навигации
- useParams для получения параметров URL

СТРУКТУРА REDUX STORE
================================================================================

store: {
  auth: {
    currentUser: User | null,
    isAuthenticated: boolean
  },
  products: {
    products: Product[]
  },
  cart: {
    items: CartItem[]
  },
  favorites: {
    products: Product[]
  }
}


================================================================================

