## **ImageFeed (ENG)**

ImageFeed is a multi-screen iOS application designed for browsing photos via the Unsplash API.

## **Links**

[Figma Design](https://www.figma.com/design/MujlanK7BDoQRrGci5G6pi/Image-Feed)

[Unsplash API](https://unsplash.com/documentation)

## **App Description**

- Authorization through Unsplash OAuth is required in the application.
- The main screen consists of a feed with images. The user can browse it, add and remove images from favorites.
- Users can view each image separately and share a link to them outside the application.
- The user has a profile with favorite images and brief information about the user.
- The application has two versions: extended and basic. In the extended version, the favorites mechanics and the ability to like photos when viewing the image in full screen are added.

### **Goals of the application**

- Viewing an infinite feed of pictures from Unsplash Editorial.
- Viewing brief information from the user’s profile.

## **Non-functional Requirements**

### **Technical Requirements**

1) Authorization works through Unsplash OAuth and a POST request to obtain an Auth Token.
2) The feed is implemented using UITableView.
3) The application uses UIImageView, UIButton, UILabel, TabBarController, NavigationController, NavigationBar, UITableView, UITableViewCell.
4) The application must support iPhone devices with iOS 15 or higher, portrait mode only.
5) All fonts in the application are system fonts (e.g. iOS 15 - SF Pro, but in future versions it may change).

## **Functional Requirements**

### **Authorization via OAuth**

To enter the application, the user must authorize via OAuth.

### *The authorization screen contains:*
1) The app logo
2) The “Log In” button

### *Algorithms and available actions:*
1) When entering the application, the user sees the splash screen;
2) After the application loads, a screen with the ability to authorize opens;
    - When pressing the “Log In” button, the browser opens on the Unsplash authorization page;
        - When pressing the “Login” button, the browser closes. The app shows a loading screen;
        - If authorization through OAuth Unsplash is not configured, pressing the login button does nothing;
        - If authorization through OAuth Unsplash is configured incorrectly - the user will not be able to enter the application;
        - On an unsuccessful login attempt, a modal error window appears;
            - When pressing “OK”, the user goes back to the authorization screen;
        - If authorization succeeds, the browser closes. The feed screen opens in the application.

### **Viewing the Feed**

In the feed, the user can view images in the feed, go to viewing a separate image, and add them to favorites.

### *The feed screen contains:*
1) A card with an image;
    - Like button;
    - Photo upload date;
2) Tab bar for navigation between the feed and the profile.

### *Algorithms and available actions:*
1) The feed screen opens by default after entering the application;
2) The feed contains images from Unsplash Editorial;
3) When scrolling down and up, the user can browse the feed;
    - If the image has not loaded yet, the system loader is shown;
    - If the image cannot be loaded - the user sees a placeholder instead of the image;
4) When pressing the Like button (gray heart) the user can like the image. After pressing, a loader is displayed:
    - If the request is successful, the loader disappears, and the icon changes to the Red Like Button (red heart).
    - If the request is unsuccessful, a modal error window appears "try again";
5) The user can remove the like by pressing the Like button again (red heart). After pressing, a loader is displayed:
    - If the request is successful, the loader disappears, and the icon changes to a gray heart.
    - If the request is unsuccessful, a modal error window appears "try again";
6) When pressing the card with the image, it will be enlarged to the boundaries of the phone and the user will go to the image viewing screen (section “Viewing the Image in Full Screen”);
7) When pressing the profile icon, the user can go to the profile;
8) The user can switch between the feed and profile screens using the tab bar.

### **Viewing the Image in Full Screen**

From the feed, the user can go to viewing the image in full screen and share it.

### *The screen contains:*
1) Enlarged image to the boundaries of the phone;
2) Button to return to the previous screen;
3) Button for downloading the image and with the ability to share it.

### *Algorithms and available actions:*
1) When opening the image in full screen, the user sees the stretched image to the boundaries of the screen. The image is centered;
    - If the image cannot be loaded and displayed - the user sees a placeholder;
    - If the response to the request is not received - a system alert with an error appears;
2) When pressing the Back button, the user can return to the feed screen;
3) With the help of gestures, the user can move around the stretched image, zoom and rotate the image. The image is fixed in the selected position;
    - If gestures for zooming or rotating the image are not configured - these actions will not be available;
4) When pressing the Share button, a system menu pops up, where the user can download the image or share it;
    - After performing the action, the menu hides;
    - The user can close the menu by swiping down or by pressing the close button;
    - If opening the system menu when pressing the “download or share image” button is not configured - it will not be displayed;

### **Viewing the User Profile**

The user can go to their profile to view the profile data or log out.

### *The profile screen contains:*
1) Profile data;
    - User photo;
    - User’s name and username;
    - Information about themselves;
2) Log out button;
3) Tab bar;

### *Algorithms and available actions:*
1) Profile data is loaded from the profile in Unsplash. Profile data cannot be changed in the application;
    - If the profile data did not load from Unsplash, the user sees a placeholder instead of the avatar. Username and name are not displayed;
2) When pressing the log out button, the user can exit the application. A system alert appears with confirmation of exit;
    - If the user presses “Yes”, then they are logged out and the authorization screen opens;
        - If the actions for the “Yes” button are not configured or configured incorrectly, then when pressing it the user is not logged out and does not get to the authorization screen;
    - If the user presses “No”, then they return to the profile screen;
    - If the alert is not configured, then when pressing the log out button nothing happens, and the user cannot log out;
3) The user can switch between the feed and profile screens using the tab bar.

## **Extended Version**

### **Adding an Image to Favorites**

In the extended version of the application, when pressing the like button, the user adds the image to favorites. Favorites are displayed in the user’s profile.

1) When pressing the Like button (gray heart), the application sends a request to add the image to favorites (without showing a loading indicator). If the request is successful, the icon changes its state and the image is added to favorites;
    - If the request to like is unsuccessful, the icon does not change its state. The image is not added to favorites;
    - If the request to add to favorites is unsuccessful, the icon does not change its state. The like is not added;
2) When pressing the Like button again (red heart), the user can remove the image from favorites;
    - If the request to remove the like is unsuccessful, the icon does not change its state. The image is not removed from favorites;
    - If the request to remove the image from favorites is unsuccessful, the icon does not change its state. The like is not removed;
3) The user can add the image to favorites when viewing the image in full screen. In the extended version, the like icon is added;
4) The user can view favorites in the profile. Favorites are displayed under the user data.
    - Next to the “Favorites” title, a counter with the number of images is displayed;
    - When scrolling down and up, the user can browse the feed with favorite photos. Profile data is not fixed and hides when scrolling;
        - If the image has not loaded yet, the system loader is displayed;
        - If the image cannot be loaded - the user sees a placeholder instead of the image;
        - If the photos are absent, the user sees a placeholder;
    - When pressing the Like button, the user can remove the image from favorites. In the main feed the like will also be removed;
    - The user can view the image in full screen;

==============================

## **ImageFeed (RUS)**

ImageFeed - это многостраничное приложение предназначенное для просмотра изображений через API Unsplash.

## **Ссылки**

[Макет Figma](https://www.figma.com/design/MujlanK7BDoQRrGci5G6pi/Image-Feed)

[API Unsplash](https://unsplash.com/documentation)

## **Описание приложения**

- В приложении обязательна авторизация через OAuth Unsplash.
- Главный экран состоит из ленты с изображениями. Пользователь может просматривать ее, добавлять и удалять изображения из избранного.
- Пользователи могут просматривать каждое изображение отдельно и делиться ссылкой на них за пределами приложения.
- У пользователя есть профиль с избранными изображениями и краткой информацией о пользователе.
- У приложения есть две версии: расширенная и базовая. В расширенной версии добавляется механика избранного и возможность лайкать фотографии при просмотре изображения на весь экран.

### **Цели приложения**

- Просмотр бесконечной ленты картинок из Unsplash Editorial.
- Просмотр краткой информации из профиля пользователя.

## **Нефункциональные требования**

### **Технические требования**

1) Авторизация работает через OAuth Unsplash и POST запрос для получения Auth Token.
2) Лента реализована с помощью UITableView.
3) В приложении использованы UImageView, UIButton, UILabel, TabBarController, NavigationController, NavigationBar, UITableView, UITableViewCell.
4) Приложение должно поддерживать устройства iPhone с iOS 15 или выше, предусмотрен только портретный режим.
5) Все шрифты в приложении - системные (ex. iOS 15 - SF Pro, но в будущих версиях он может поменяться).

## **Функциональные требования**

### **Авторизация через OAuth**

Для входа в приложение пользователь должен авторизоваться через OAuth.

### *Экран авторизации содержит:*
1) Логотип приложения
2) Кнопку «Войти»

### *Алгоритмы и доступные действия:*
1) При входе в приложение пользователь видит splash-screen;
2) После загрузки приложения открывается экран с возможностью авторизации;
    - При нажатии на кнопку «Войти» открывается браузер на странице авторизации Unsplash;
        - При нажатии на кнопку «Login» браузер закрывается. В приложении появляется экран загрузки;
        - Если авторизация через OAuth Unsplash не настроена, по нажатию на кнопку логина ничего не происходит;
        - Если авторизация через OAuth Unsplash настроена не корректно - пользователь не сможет войти в приложение;
        - При неудачной попытке входа всплывает модальное окно с ошибкой;
            - При нажатии на «ОК» пользователь переходит обратно на экран авторизации;
        - Если авторизация прошла успешно, то браузер закрывается. В приложении открывается экран с лентой.

### **Просмотр ленты**

В ленте пользователь может просматривать изображения в ленте, переходить к просмотру отдельного изображения и добавлять их в избранное.

### *Экран ленты содержит:*
1) Карточку с изображением;
    - Кнопку Лайк;
    - Дата загрузки фотографии;
2) Таб бар для навигации между лентой и профилем.

### *Алгоритмы и доступные действия:*
1) Экран с лентой открывается по умолчанию после входа в приложение;
2) Лента содержит изображения из Unsplash Editorial;
3) При скролле вниз и вверх пользователь может просматривать ленту;
    - Если изображение не успело загрузиться, то пользователю отображается системный лоадер;
    - Если изображение невозможно загрузить - пользователь видит плэйсхолдер вместо изображения;
4) При нажатии на кнопку Лайк (серое сердечко) пользователь может лайнкуть изображение. После нажатия отображается лоадер:
    - Если запрос успешный, то лоадер пропадает, иконка меняет состояние на Кнопку Красный Лайк (красное сердечко).
    - Если запрос не успешный, то всплывает модальное окно с ошибкой «попробуйте еще раз»
5) Пользователь может убрать лайк, повторно нажав на кнопку Лайк (красное сердечко). После нажатия отображается лоадер:
    - Если запрос успешный, то лоадер пропадает, иконка меняет состояние на серое сердечко.
    - Если запрос не успешный, то всплывает модальное окно с ошибкой «попробуйте еще раз»;
6) При нажатии на карточку с изображением оно увеличится до границ телефона и пользователь перейдет на экран просмотра изображения (раздел «Просмотр изображения на весь экран»);
7) При нажатии на иконку профиля пользователь может перейти в профиль;
8) Пользователь может переключаться между экранами ленты и профиля с помощью таб бара.

### **Просмотр изображения на весь экран**

Из ленты пользователь может перейти к просмотру изображения на весь экран и поделиться им.

### *Экран содержит:*
1) Увеличенное изображение до границ телефона;
2) Кнопку возврата на предыдущий экран;
3) Кнопку для загрузки изображения и с возможностью им поделиться.

### *Алгоритмы и доступные действия:*
1) При открытии изображения на весь экран пользователь видит растянутое изображение до границ экрана. Изображение выровнено по центру;
    - Если изображение невозможно загрузить и показать - пользователь видит плэйсхолдер;
    - Если ответ на запрос не получен - появляется системный алерт с ошибкой;
2) При нажатии на кнопку Назад пользователь может вернуться на экран просмотра ленты;
3) При помощи жестов пользователь может перемещаться по растянутому изображению, зумировать и поворачивать изображение. Изображение фиксируется в выбранном положении;
    - Если не настроены жесты для увеличения или поворота изображения - эти действия будут не доступны;
4) При нажатии на кнопку кнопку Поделиться всплывает системное меню, в котором пользователь может загрузить изображение или поделиться им;
    - После совершения действия меню скрывается;
    - Пользователь может закрыть меню свайпом вниз или при нажатии на крестик;
    - Если открытие системного меню при нажатии на кнопку “загрузить или поделиться изображением” не настроено - оно не будет показываться;

### **Просмотр профиля пользователя**

Пользователь может перейти в свой профиль, чтобы посмотреть данные профиля или выйти из него.

### *Экран профиля содержит:*
1) Данные профиля;
    - Фотографию пользователя;
    - Имя и username пользователя;
    - Информация о себе;
2) Кнопку выхода из профиля;
3) Таб бар;

### *Алгоритмы и доступные действия:*
1) Данные профиля загружаются из профиля в Unsplash. Данные профиля нельзя изменить в приложении;
    - Если данные профиля не подтянулись из Unsplash, то пользователь видит плэйсхолдер вместо аватрки. Username и имя не отображаются;
2) При нажатии на кнопку выхода из профиля (логаут) пользователь может выйти из приложения. Всплывает системный алерт с подтверждением выхода;
    - Если пользователь нажимает «Да», то он разлогинивается и открывается экран авторизации;
        - Если не настроены или настроены неправильно действия с кнопкой «Да», то при нажатии пользователя не разлогинивается и попадает на экран авторизации;
    - Если пользователь нажимает «Нет», то он возвращается на экран профиля;
    - Если алерт не настроен, то при нажатии на кнопку выходы ничего не происходит, пользователь не может разлогиниться;
3) Пользователь может переключаться между экранами ленты и профиля с помощью таб бара.

## **Расширенная версия**

### **Добавление изображения в избранное**

В расширенной версии приложения при нажатии на лайк пользователь добавляет изображение в избранное. Избранное отображается в профиле пользователя.

1) При нажатии на кнопку Лайк (серое сердечко) приложение делает запрос на добавление изображения в избранное (не показывая индикатор загрузки). При успешном запросе иконка меняет состояние и изображение добавляется в избранное;
    - Если запрос на лайк неуспешный, то иконка не меняет свое состояние. Изображение в избранное не добавляется;
    - Если запрос на добавление в избранное неуспешный, то иконка не меняет свое состояние. Лайк не ставится;
2) При повторном нажатии на кнопку Лайк (красное сердечко) пользователь может удалить изображение из избранного;
    - Если запрос на удаление лайка неуспешный, то иконка не меняет свое состояние. Изображение не удаляется из избранного;
    - Если запрос на удаление изображения из избранного неуспешный, то иконка не меняет свое состояние. Лайк не удаляется;
3) Пользователь может добавить изображение в избранное при просмотре изображения на весь экран. В расширенной версии добавляется иконка лайка;
4) Пользователь может просмотреть избранное в профиле. Избранное отображается под данными пользователя.
    - Рядом с заголовком «Избранное» отображается счетчик количества изображений;
    - При скролле вниз и вверх пользователь может просматривать ленту с избранными фотографиями. Данные профиля не зафиксированы и скрываются при скролле;
        - Если изображение не успело загрузиться, то пользователю отображается системный лоадер;
        - Если изображение невозможно загрузить - пользователь видит плэйсхолдер вместо изображения;
        - Если фотографии отсутствуют, то пользователь видит плэйсхолдер;
    - При нажатии на кнопку Лайк пользователь может удалить изображение из избранного. В основной ленте лайк тоже удалится;
    - Пользователь может просмотреть изображение на весь экран;
