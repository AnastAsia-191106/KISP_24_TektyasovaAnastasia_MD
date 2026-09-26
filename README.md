## Тема: Использование React Native и Expo 

  **Цель этого урока** - начать с Expo и познакомиться с Expo SDK. Он будет охватывать следующие темы:

* Создать приложение с помощью шаблона по умолчанию с включенным типом Скриптом
* Реализуйте двухэкранный макет нижних вкладок с помощью Expo Router
* Разбейте макет приложения и реализуйте его с помощью flexbox
* Используйте пользовательский интерфейс системы каждой платформы для выбора изображения из медиа-библиотеки
* Создайте модаль наклейки с помощью <Modal> и <FlatList> Компоненты от React Native
* Добавьте сенсорные жесты, чтобы взаимодействовать со стикером
* Используйте сторонние библиотеки, чтобы захватить скриншот и сохранить его на диске
* Обработка различий в платформе между Android, iOS и Web
* Наконец, пройдите процесс настройки панели состояния, экрана брызг и значка для завершения приложения.

Эти темы обеспечивают основу для изучения основ создания приложения Expo. Учебник является самостоятельным и может занять до двух часов.

Чтобы сохранить его для начинающих, мы разделили учебник на девять глав, чтобы вы могли следовать или положить его и вернуться к нему позже. Каждая глава содержит необходимые фрагменты кода для выполнения шагов, поэтому вы можете следовать за ним, создавая приложение с нуля или копировать и вставлять его.

Прежде чем мы начнем, взгляните на то, что мы построим. Это приложение под названием StickerSmash, которое работает на Android, iOS и в Интернете:
Как использовать этот учебник

Мы верим в обучение, поэтому этот учебник подчеркивает, что делаем, а не объясняя. Вы можете следить за ходом создания приложения, создавая приложение с нуля.

На протяжении всего урока любой важный код или код, которые изменились между примерами, будут выделены зеленым цветом. Вы можете навести курсор на основные моменты (на рабочем столе) или нажать на них (на мобильном телефоне), чтобы узнать больше об изменении. Например, код, выделенный в фрагменте ниже, объясняет, что он делает:

````
import { StyleSheet, Text, View } from 'react-native';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text>Hello world!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
````
## Тема: Создайте свое первое приложение
Инициализировать новое приложение Expo

Мы будем использовать create-expo-app Инициализировать новое приложение Expo. Это командный инструмент для создания нового проекта React Native. Запустите следующую команду в вашем терминале:
````
npx create-expo-app@latest StickerSmash
Select an Expo SDK version > SDK 57
cd StickerSmash
````

Эта команда создаст новый каталог проекта под названием StickerSmash, используя шаблон по умолчанию. Этот шаблон имеет необходимый шаблонный код и библиотеки, необходимые для создания нашего приложения, включая Expo Router, и позволяет нам тестировать наше приложение с помощью Expo Go, установленного на наших устройствах. Мы будем продолжать добавлять больше библиотек в этом уроке по мере необходимости.

## Скачать активы

После загрузки архива:
Расчистите архив и замените активы по умолчанию в ````your-project-name/assets/imagesкаталоге```` ````«Ваш-проект-имя/активы/изображения»````.
Откройте каталог проекта в редакторе кода или IDE.
Запустить сценарий сброса-проекта

В этом уроке мы создадим наше приложение с нуля и поймем основы добавления файловой навигации. Давайте запустим ```reset-project ```скрипт для удаления кода шаблона:
````
npm run reset-project
````
После выполнения вышеуказанной команды в каталоге `src/app осталось два файла (index.tsx и _layout.tsx)`. Предыдущие файлы из каталога src (включая componentsкомпоненты, константы и зацепки) перемещаются в диаграмму по сценарию. Мы создадим наши собственные каталоги и составные файлы по мере продвижения.
Что делает `reset-projectСценарий` делает?

reset-project script resets the src/app directory structure in a project and moves the previous boilerplate files from the project's src directory to another sub-directory called example. We can delete it since it is not part of our main app's structure.

4 Запуск приложения на мобильном и веб-сайте

В каталоге проекта запустите следующую команду для запуска сервера разработки с терминала:
Терминал
````
npx expo start
````
После выполнения вышеуказанной команды:
1. Завершится сервер разработки, и вы увидите QR-код внутри окна терминала.
2. Сканируйте этот QR-код, чтобы открыть приложение на устройстве. На Android используйте опцию Expo Go > Scan QR-кода. На iOS используйте приложение камеры по умолчанию.
3. Чтобы запустить веб-приложение, нажмите W В терминале. Он откроет веб-приложение в веб-браузере по умолчанию.


5
Редактировать индексный экран

 `src/app/index.tsx` файл определяет текст, отображаемый на экране приложения. Это точка входа нашего приложения и выполняет, когда сервер разработки начинается. Он использует основные компоненты React Native, такие как <View> и <Text> для отображения фона и текста.

Стили, применяемые к этим компонентам, используют объекты JavaScript, а не CSS, который используется в Интернете. Тем не менее, многие свойства будут выглядеть знакомыми, если вы ранее использовали CSS в Интернете. Большинство реагированных народные компоненты принимают style реквизит, который принимает объект JavaScript в качестве его значения. Для получения более подробной информации см. Стиль в React Native.

Давайте изменим экран **`src/app/index.tsx`**:
1. Импорт `StyleSheet` от `react-native` и создать a `styles` Возражает, чтобы определить наши пользовательские стили.
2. Добавить a `styles.container.backgroundColor` собственность для `<View>` с ценностью `#25292e`. Это меняет цвет фона.
3. Заменить значение по умолчанию `<Text>` с "Домашний экран".
4. Добавить a `styles.text.color` собственность для `<Text>` с ценностью `#fff` (белый) для изменения цвета текста.

**src/app/index.tsx**
```
import { Text, View, StyleSheet } from 'react-native';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    color: '#fff',
  },
});
````

## Тема: Добавить навигацию

## Основы экс-маршрутизатора
**Expo Router** - это файловая система маршрутизации для React Native и веб-приложений. Он управляет навигацией между экранами и использует одни и те же компоненты на нескольких платформах. Чтобы начать работу, нам нужно знать о следующих конвенциях:

* Каталог приложений: Специальный каталог, содержащий только маршруты и их макеты. Любые файлы, добавленные в этот каталог, становятся экраном в нашем родном приложении и страницей в Интернете. В шаблоне по умолчанию он расположен в src/app.
* Корневой макет : файл src/app/_layout.tsx. Он определяет общие элементы пользовательского интерфейса, такие как заголовки и панели вкладок, чтобы они были согласованы между различными маршрутами.
* Названия файлов Convention: Индекс Файлы имен, такие как index.tsx, сопоставьте свой родительский каталог и не добавляйте сегмент пути. Например, к примеру, index.tsx Файл в src/приложение Справочник матчей / Маршрут.
* А маршрут Файл экспортирует компонент React в качестве его значения по умолчанию. Он может использовать любой .js, .jsx, .ts, или .tsx Расширение.
* Android, iOS и веб разделяют единую структуру навигации.

## Добавить новый экран в стек

Давайте создадим новый файл с именем `о.tsx` внутри `src/приложение` Каталог. Он отображает имя экрана, когда пользователь переходит к `/about` Маршрут.

**src/app/about.tsx**
````
import { Text, View, StyleSheet } from 'react-native';

export default function AboutScreen() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>About screen</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    color: '#fff',
  },
});
````

**Внутри `src/app/_layout.tsx` :**

1. Добавить a <Stack.Screen /> Компонент и a options реквизит для обновления заголовка /about Маршрут.
2. Обновить /index Название маршрута на Home путем добавления options Прокв.

**src/app/_layout.tsx**
````
import { Stack } from 'expo-router';

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ title: 'Home' }} />
      <Stack.Screen name="about" options={{ title: 'About' }} />
    </Stack>
  );
}
````
## Навигация между экранами
Мы будем использовать Expo Router's `Link` компонент для навигации от `/index` Маршрут к `/about` Маршрут. Это компонент React, который отображает `<Text>` С данностью href Прокв.

1. Импортировать `Link` компонент из expo-router внутри `src/app/index.tsx`.
2. Добавить a `Link` компонент после `<Text>` компонент и пропуск href реквизит с `/about` Маршрут.
3. Добавить стиль `fontSize`, `textDecorationLine`, и `color` к `Link` компонент. Он принимает тот же реквизит, что и `<Text>` компонент.

**src/app/index.tsx**
````
import { Text, View, StyleSheet } from 'react-native';
import { Link } from 'expo-router';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
      <Link href="/about" style={styles.button}>
        Go to About screen
      </Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    color: '#fff',
  },
  button: {
    fontSize: 20,
    textDecorationLine: 'underline',
    color: '#fff',
  },
});
````
## Добавить не найденный маршрут

Когда маршрут не существует, мы можем использовать +not-found Маршрут для отображения запасного экрана. Это полезно, когда мы хотим отобразить пользовательский экран при навигации по неверному маршруту на мобильном телефоне вместо того, чтобы сбивать приложение или отображать 404 Ошибка в Интернете. Экспо Роутер использует специальный `+not-found.tsx` файл для рассмотрения этого дела.

1. Создать новый файл с именем `+not-found.tsx `внутри `src/приложение` Каталог для добавления NotFoundScreen компонент.
2. Добавить `options` реквизит от `Stack.Screen` для отображения пользовательского заголовка экрана для этого маршрута.
3. Добавить a `Link` Компонент для перехода к `/` Маршрут, который является нашим запасным маршрутом.

**src/app/+not-found.tsx**
````
import { View, StyleSheet } from 'react-native';
import { Link, Stack } from 'expo-router';

export default function NotFoundScreen() {
  return (
    <>
      <Stack.Screen options={{ title: 'Oops! Not Found' }} />
      <View style={styles.container}>
        <Link href="/" style={styles.button}>
          Go back to Home screen!
        </Link>
      </View>
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    justifyContent: 'center',
    alignItems: 'center',
  },

  button: {
    fontSize: 20,
    textDecorationLine: 'underline',
    color: '#fff',
  },
});
````
## Добавить навигатор нижней вкладки
На данный момент структура файлов нашего каталога src/app выглядит следующим образом:
```
src
 
app
  
_layout.tsx
Root layout
  
index.tsx
matches route '/'
  
about.tsx
matches route '/about'
  
+not-found.tsx
matches route any 404 route
````
Мы добавим навигатор нижней вкладки в наше приложение и повторно используем существующие экраны `Home` и `About` для создания макета вкладки (общий шаблон навигации во многих приложениях социальных сетей, таких как `X` или `BlueSky`). Мы также будем использовать навигатор стека в макете `Root`, так что `+not-found` маршрут отображается над любыми другими вложенными навигаторами.

    Внутри каталога `src/app` добавить (вкладки) подкаталог. Этот специальный каталог используется для группирования маршрутов вместе и отображения их в нижней строке вкладок.
    Создайте файл `(tabs)/_layout.tsx` внутри каталога. Он будет использоваться для определения макета вкладки, который отделен от макета `Root`.
    Переместите существующие файлы `index.tsx` и `about.tsx` в каталог (вкладки). Структура каталога `src/app` будет выглядеть так:
````
src
 
app
  
_layout.tsx
Root layout
  
+not-found.tsx
matches route any 404 route
  
(tabs)
   
_layout.tsx
Tab layout
   
index.tsx
matches route '/'
   
about.tsx
matches route '/about'
````
Обновите файл макета `Root`, чтобы добавить a (`tabs`) Маршрут:

**src/app/_layout.tsx**
````
import { Stack } from 'expo-router';

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
    </Stack>
  );
}
````
Внутри (таблицы)`/_layout.tsx`, добавить a `Tabs` компонент для определения макет нижней вкладки:

**src/app/(tabs)/_layout.tsx**

````
import { Tabs } from 'expo-router';

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen name="index" options={{ title: 'Home' }} />
      <Tabs.Screen name="about" options={{ title: 'About' }} />
    </Tabs>
  );
}
````
## Установить @expo/vector-icons
Чтобы установить `@expo/vector-icons` библиотека, остановите сервер разработки, нажав `Ctrl + C` в терминале, затем запустить следующую команду:
````
npx expo install @expo/vector-icons
````
После завершения установки запустите сервер разработки, запустив `npx expo start`.

## Обновление нижнего вкладки навигатора

Прямо сейчас нижний навигатор вкладки выглядит одинаково на всех платформах, но не соответствует стилю нашего приложения. Например, панель вкладки или заголовок не отображает пользовательский значок, а цвет фоновой вкладки нижней части не соответствует цвету фона приложения.

Измените файл `src/app/(tabs)/_layout.tsx`, чтобы добавить значки панели вкладок:

1. Импорт `Ionicons` Иконки набор из `@expo/vector-icons` — библиотека, включающая в себя популярные наборы значков.
2. Добавить `tabBarIcon` для обоих `index` и `about` Маршруты. Эта функция принимает `focused` и `color` как парам и отображает компонент значка. Из набора иконок мы можем предоставить пользовательские имена значков.
3. Добавить `screenOptions.tabBarActiveTintColor` к `Tabs` компонент и установить его значение для `#ffd33d`. Это изменит цвет значка икета вкладки и этикетку при активном.

**src/app/(tabs)/_layout.tsx**
````
import { Tabs } from 'expo-router';
import Ionicons from '@expo/vector-icons/Ionicons';

export default function TabLayout() {
  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: '#ffd33d',
      }}
    >
      <Tabs.Screen
        name="index"
        options={{
          title: 'Home',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'home-sharp' : 'home-outline'} color={color} size={24} />
          ),
        }}
      />
      <Tabs.Screen
        name="about"
        options={{
          title: 'About',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'information-circle' : 'information-circle-outline'} color={color} size={24}/>
          ),
        }}
      />
    </Tabs>
  );
}
````

Давайте также изменим цвет фона панели вкладок и заголовка с помощью `screenOptions` реквизит:

**src/app/(tabs)/_layout.tsx**

````
<Tabs
  screenOptions={{
    tabBarActiveTintColor: '#ffd33d',
    headerStyle: {
      backgroundColor: '#25292e',
    },
    headerShadowVisible: false,
    headerTintColor: '#fff',
    tabBarStyle: {
      backgroundColor: '#25292e',
    },
  }}
>
````
В вышеуказанном коде:

* Предыстория заголовка установлена на `#25292e` с помощью `headerStyle` собственность. Мы также отключили тень заголовка, используя headerShadowVisible.
* `headerTintColor` Применяется `#fff` к этикетке заголовка
* `tabBarStyle.backgroundColo`r Применяется `#25292e` к вкладке бар

## Тема: Создайте экран

В этой главе мы создадим первый экран приложения StickerSmash.

## Разбейте экран
Прежде чем мы создадим этот экран, написав код, давайте разберем его на некоторые важные элементы.
Есть два основных элемента:

* В центре экрана отображается большое изображение
* В нижней половине экрана есть две кнопки

Первая кнопка содержит несколько компонентов. Основополагающий элемент обеспечивает желтую границу и содержит значок и текстовые компоненты внутри ряда.

Теперь, когда мы разбили пользовательский интерфейс на более мелкие куски, мы готовы начать кодирование.

## Отобразить изображение

Мы будем использовать `expo-image` библиотека для отображения изображения в приложении. Он обеспечивает кроссплатформенную `<Image>` компонент для загрузки и визуализации изображения. Он уже включен в шаблон проекта по умолчанию, который мы используем.

Компонент изображения берет источник изображения в качестве его значения. Источник может быть либо `Статический актив` или URL. Например, источник, необходимый от **активы/изображения**. 
**Каталог** - это статично. Это также может быть от `Сеть` как а `uri` собственность.

Для использования компонента Изображения в src/app/(tabs)/index.tsx файл:

1. Импорт `Image` от `expo-image` Библиотека.
2. Создать a `PlaceholderImage` переменная для использования **`активы/images/background-image.png`** файл как source Опора на Ima`ge компонент.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';
import { Image } from 'expo-image';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <Image source={PlaceholderImage} style={styles.image} />
      </View>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
````
## Разделить компоненты на файлы

Давайте разделим код на несколько файлов, так как мы добавляем больше компонентов на этот экран. На протяжении всего этого урока мы будем использовать каталог компонентов для создания пользовательских компонентов.

1. Создайте каталог компонентов внутри src, а внутри него создайте файл image-viewer.tsx.
2. Переместить код, чтобы отобразить изображение в этом файле вместе с image Стили.

**src/components/image-viewer.tsx**
````
import { ImageSourcePropType, StyleSheet } from 'react-native';
import { Image } from 'expo-image';

type Props = {
  imgSource: ImageSourcePropType;
};

export default function ImageViewer({ imgSource }: Props) {
  return <Image source={imgSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
````

Импорт `ImageViewer` и использовать его в `src/app/(tabs)/index.tsx`:

**src/app/(tabs)/index.tsx**
````
import { StyleSheet, View } from 'react-native';

import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
});
````
## Создать кнопки с помощью прессов

`React Native` включает в себя несколько различных компонентов для обработки сенсорных событий, но `<Pressable>` Рекомендуется для его гибкости. Он может обнаруживать отдельные нажатия, длинные нажатия, срабатывать отдельные события, когда кнопка нажимается и освобождается, и многое другое.

В дизайне есть две кнопки, которые нам нужно создать. Каждый из них имеет свой стиль и этикетку. Давайте начнем с создания многоразового компонента для этих кнопок. Создайте файл `button.tsx` внутри каталога `src/components` с помощью следующего кода:

**src/components/button.tsx**
````
import { StyleSheet, View, Pressable, Text } from 'react-native';

type Props = {
  label: string;
};

export default function Button({ label }: Props) {
  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={() => alert('You pressed a button.')}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 320,
    height: 68,
    marginHorizontal: 20,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: '100%',
    height: '100%',
    alignItems: 'center',
    justifyContent: 'center',
    flexDirection: 'row',
  },
  buttonLabel: {
    color: '#fff',
    fontSize: 16,
  },
});
````

Приложение отображает оповещение, когда пользователь нажимает любую из кнопок на экране. Это происходит потому, что `<Pressable>` звонки alert() на его onPress Прокв. Давайте импортируем этот компонент в src/app/(tabs)/index.tsx файл и добавить стили для `<View>` которые инкапсулируют эти кнопки:

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require("@/assets/images/background-image.png");

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button label="Choose a photo" />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
});
````

Давайте посмотрим на наше приложение на Android, iOS и в Интернете:
Первоначальный макет.

Вторая кнопка с этикеткой **"Используйте эту фотографию"** напоминает фактическую кнопку от дизайна. Тем не менее, первая кнопка требует большего стиля, чтобы соответствовать дизайну.

## Улучшить многоразовый компонент кнопки

Кнопка **«Выберите фотографию»** требует другого стиля, чем кнопка **«Использовать эту фотографию»**, поэтому мы добавим новый реквизит кнопки, который позволит нам применять primary Тема. Эта кнопка также имеет иконку перед этикеткой. Мы будем использовать иконку из `@expo/vector-icons` Библиотека.

Чтобы загрузить и отобразить значок на кнопке, давайте использовать `FontAwesome` Из библиотеки. Изменить `src/components/button.tsx` для добавления следующего фрагмента кода:

**src/components/button.tsx**
````
import { StyleSheet, View, Pressable, Text } from 'react-native';
import FontAwesome from '@expo/vector-icons/FontAwesome';

type Props = {
  label: string;
  theme?: 'primary';
};

export default function Button({ label, theme }: Props) {
  if (theme === 'primary') {
  return (
      <View
        style={[
          styles.buttonContainer,
          { borderWidth: 4, borderColor: '#ffd33d', borderRadius: 18 },
        ]}>
        <Pressable
          style={[styles.button, { backgroundColor: '#fff' }]}
          onPress={() => alert('You pressed a button.')}>
          <FontAwesome name="picture-o" size={18} color="#25292e" style={styles.buttonIcon} />
          <Text style={[styles.buttonLabel, { color: '#25292e' }]}>{label}</Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={() => alert('You pressed a button.')}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 320,
    height: 68,
    marginHorizontal: 20,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: '100%',
    height: '100%',
    alignItems: 'center',
    justifyContent: 'center',
    flexDirection: 'row',
  },
  buttonIcon: {
    paddingRight: 8,
  },
  buttonLabel: {
    color: '#fff',
    fontSize: 16,
  },
});
````

Давайте узнаем, что делает вышеприведенный код:

* Кнопка основной темы использует винные стили, который переопределяет стили, определенные в StyleSheet.create() с предметом, непосредственно переданным в style Прокв.
* The <Pressable> компонент в первичной теме использует backgroundColor Собственность со значением #fff чтобы установить фон кнопки на белый. Если мы добавим это свойство к styles.button, значение цвета фона будет установлено как для основной темы, так и для нестилейной.
* Встроенные стили используют JavaScript и переопределяют стили по умолчанию для определенного значения.

А теперь, измените `src/app/(tabs)/index.tsx` файл для использования `theme="primary"` Реквизит на первой кнопке.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button theme="primary" label="Choose a photo" />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
});
````
## Тема: Использовать сборщик изображений
## Установить expo-image-Picker
Чтобы установить `expo-image-picker` библиотека, остановите сервер разработки, нажав `Ctrl + C` в терминале, затем запустить следующую команду:
````
npx expo install expo-image-picker
````
The `npx expo install` команда установит библиотеку и добавит ее в зависимости проекта в `package.json`.

## Выберите изображение из медиа-библиотеки устройства

`expo-image-picker` обеспечивает `launchImageLibraryAsync()` способ отображения пользовательского интерфейса системы путем выбора изображения или видео из медиа-библиотеки устройства. Мы будем использовать основную тематическую кнопку, созданную в предыдущей главе, чтобы выбрать изображение из медиа-библиотеки устройства и создать функцию для запуска библиотеки изображений устройства для реализации этой функции.

В `src/app/(tabs)/index.tsx`, импорт `expo-image-picker` библиотека и создать `pickImageAsync()` Функция внутри `Index` компонент:

**src/app/(tabs)/index.tsx**
```
// ...rest of the import statements remain unchanged
import * as ImagePicker from 'expo-image-picker';

export default function Index() {
  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      console.log(result);
    } else {
      alert('You did not select any image.');
    }
  };

  // ...rest of the code remains same
}
````
Давайте узнаем, что делает вышеприведенный код:

* The launchImageLibraryAsync() принимает объект для указания различных опций. Этот объект является ImagePickerOptions объект, который мы передаем при вызове метода.
* Когда allowsEditing настроено на true, пользователь может обрезать изображение во время процесса выбора на Android и iOS.

## Обновите компонент кнопки

При нажатии основной кнопки мы позвоним `pickImageAsync()` Функция на Button компонент. Обновить onPress реквизит The Button компонент в `src/components/button.tsx`:

**src/components/button.tsx**
````
import { StyleSheet, View, Pressable, Text } from 'react-native';
import FontAwesome from '@expo/vector-icons/FontAwesome';

type Props = {
  label: string;
  theme?: 'primary';
  onPress?: () => void;
};

export default function Button({ label, theme, onPress }: Props) {
  if (theme === 'primary') {
    return (
      <View
        style={[
          styles.buttonContainer,
          { borderWidth: 4, borderColor: '#ffd33d', borderRadius: 18 },
        ]}>
        <Pressable style={[styles.button, { backgroundColor: '#fff' }]} onPress={onPress}>
          <FontAwesome name="picture-o" size={18} color="#25292e" style={styles.buttonIcon} />
          <Text style={[styles.buttonLabel, { color: '#25292e' }]}>{label}</Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={() => alert('You pressed a button.')}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: {
    width: 320,
    height: 68,
    marginHorizontal: 20,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 3,
  },
  button: {
    borderRadius: 10,
    width: '100%',
    height: '100%',
    alignItems: 'center',
    justifyContent: 'center',
    flexDirection: 'row',
  },
  buttonIcon: {
    paddingRight: 8,
  },
  buttonLabel: {
    color: '#fff',
    fontSize: 16,
  },
});
````

В `src/app/(tabs)/index.tsx`, добавить `pickImageAsync() `Функция для onPress реквизит на первом `<Button>`.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      console.log(result);
    } else {
      alert('You did not select any image.');
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
});
````

The `pickImageAsync()` Функции вызывают `ImagePicker`.`launchImageLibraryAsync()` А затем обрабатывает результат. The `launchImageLibraryAsync()` Способ возвращает объект, содержащий информацию о выбранном изображении.

Вот пример из `result` объект и свойства, которые он содержит:
````
{
  "assets": [
    {
      "assetId": null,
      "base64": null,
      "duration": null,
      "exif": null,
      "fileName": "ea574eaa-f332-44a7-85b7-99704c22b402.jpeg",
      "fileSize": 4513577,
      "height": 4570,
      "mimeType": "image/jpeg",
      "rotation": null,
      "type": "image",
      "uri": "file:///data/user/0/host.exp.exponent/cache/ExperienceData/%2540anonymous%252FStickerSmash-13f21121-fc9d-4ec6-bf89-bf7d6165eb69/ImagePicker/ea574eaa-f332-44a7-85b7-99704c22b402.jpeg",
      "width": 2854
    }
  ],
  "canceled": false
}
````
## Использовать выбранное изображение

The `result` Объект обеспечивает `assets` массив, который содержит `uri` Выбранное изображение. Давайте возьмем это значение из сборщика изображений и используем его, чтобы показать выбранное изображение в приложении.

Изменить файл `src/app/(tbs)/index.tsx`:

1. Объявить переменную состояния, называемую selectedImage с помощью `useState` Крюк от `React`. Мы будем использовать эту переменную состояния для удержания `URI` выбранного изображения.
2. Обновить `pickImageAsync()` функция для сохранения изображения `URI` в selectedImage Переменная состояния.
3. Пройти selectedImage В качестве опоры для `ImageViewer` компонент.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
    } else {
      alert('You did not select any image.');
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
});
````

Пройти `selectedImage` Опора для `ImageViewer` компонент для отображения выбранного изображения вместо образа заполнителя.

1. Изменить `src/components/image-viewer.tsx` файл, чтобы принять `selectedImage` Прокв.
2. Источник изображения становится длинным, поэтому давайте также переместим его в отдельную переменную, называемую `imageSource`.
3. Пропуск `imageSource` как ценность `source` Опора на `Image` компонент.

**src/components/image-viewer.tsx**
````
import { ImageSourcePropType, StyleSheet } from 'react-native';
import { Image } from 'expo-image';

type Props = {
  imgSource: ImageSourcePropType;
  selectedImage?: string;
};

export default function ImageViewer({ imgSource, selectedImage }: Props) {
  const imageSource = selectedImage ? { uri: selectedImage } : imgSource;

  return <Image source={imageSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
````

В приведенном выше фрагменте компонент Изображение использует условный оператор для загрузки источника изображения. Выбранное изображение является `uri` Струнные, не локальный актив, как изображение заполнителя.

## Тема: Создать модаль

`React Native` предоставляет `<Modal>` компонент Это представляет контент выше остальной части вашего приложения. В общем, модаль используются, чтобы привлечь внимание пользователя к критической информации или направить их на принятие мер. Например, в Третья глава, после нажатия кнопки, мы использовали `alert()` для отображения текста заполнителя. Вот как модальный компонент отображает наложение.

## Объявить переменную состояния для отображения кнопок

Перед реализацией модала мы собираемся добавить три новые кнопки. Эти кнопки видны после того, как пользователь выбирает изображение из медиа-библиотеки или использует образ заполнителя. Одна из этих кнопок запустит модаль сборщика смайликов.

В `src/app/(tbs)/index.tsx` :

1. Объявить переменную булева состояния, `showAppOptions`, чтобы показать или скрыть кнопки, которые открывают модаль, наряду с несколькими другими вариантами. Когда экран приложения загружается, мы настроим его `false` Таким образом, опции не отображаются перед выбором изображения. Когда пользователь выбирает изображение или использует образ заполнителя, мы установим его `true`.
2. Обновить `pickImageAsync()` функция для установления значения `showAppOptions` к `true` После того, как пользователь выбирает изображение.
3. Обновите кнопку без темы, добавив `onPress` реквизит со следующим значением.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
      </View>
      {showAppOptions ? (
        <View />
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
});
````
В приведенном выше фрагменте мы передаем `Button` Компонент, основанный на значении `showAppOptions` и перемещение кнопок в блоке оператора тернарма. Когда ценность `showAppOptions` является `true`, сделать пустым <`View`> компонент. Мы обратимся к этому государству на следующем шаге.

Теперь мы можем удалить `alert` на `Button` компонент и обновление onPress реквизит при рендеринге второй кнопки в `src/components/button.tsx`:

**src/components/button.tsx**
````
<Pressable style={styles.button} onPress={onPress}>
````

## Добавить кнопки

Внутри каталога `src/components` создайте новый файл `circle-button.tsx` со следующим кодом:

**src/компоненты/круг-ног.тс**

````
import { View, Pressable, StyleSheet } from 'react-native';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = {
  onPress: () => void;
};

export default function CircleButton({ onPress }: Props) {
  return (
    <View style={styles.circleButtonContainer}>
      <Pressable style={styles.circleButton} onPress={onPress}>
        <MaterialIcons name="add" size={38} color="#25292e" />
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  circleButtonContainer: {
    width: 84,
    height: 84,
    marginHorizontal: 60,
    borderWidth: 4,
    borderColor: '#ffd33d',
    borderRadius: 42,
    padding: 3,
  },
  circleButton: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    borderRadius: 42,
    backgroundColor: '#fff',
  },
});
````

Чтобы отобразить значок плюс, эта кнопка использует <`MaterialIcons`> Иконный набор из `@expo/vector-icons` Библиотека.

Две другие кнопки также используют <`MaterialIcons`> для отображения вертикально выровненных текстовых меток и значков. Создать именованный файл `icon-button.tsx` внутри `src/компоненты` Каталог. Этот компонент принимает три реквизита:

* icon: имя, соответствующее `MaterialIcons` Икона библиотеки.
* label: текстовая этикетка, отображаемая на кнопке.
* onPress: эта функция вызывает, когда пользователь нажимает кнопку.

**src/компоненты/icon-button.tsx**
````
import { Pressable, StyleSheet, Text } from 'react-native';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = {
  icon: keyof typeof MaterialIcons.glyphMap;
  label: string;
  onPress: () => void;
};

export default function IconButton({ icon, label, onPress }: Props) {
  return (
    <Pressable style={styles.iconButton} onPress={onPress}>
      <MaterialIcons name={icon} size={24} color="#fff" />
      <Text style={styles.iconButtonLabel}>{label}</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  iconButton: {
    justifyContent: 'center',
    alignItems: 'center',
  },
  iconButtonLabel: {
    color: '#fff',
    marginTop: 12,
  },
});
````
Внутренний `src/app/(tbs)/index.tsx` :

1. Импортировать `CircleButton` и `IconButton` Компоненты для их отображения.
2. Добавьте три функции заполнителя для этих кнопок. The `onReset()` функции вызывают, когда пользователь нажимает кнопку сброса, в результате чего кнопка выбора изображения снова появляется. Мы добавим функциональность для двух других функций позже.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    // we will implement this later
  };

  const onSaveImageAsync = async () => {
    // we will implement this later
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
  optionsContainer: {
    position: 'absolute',
    bottom: 80,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
});
```
## Создать модаль сборщика смайликов

Модаль позволяет пользователю выбрать эмодзи из списка доступных эмодзи. Создайте файл `emoji-picker.tsx` внутри каталога `src/components`. Этот компонент принимает три реквизита:

* isVisible: бульон для определения состояния видимости модала.
* onClose: функция, чтобы закрыть модаль.
* children: используется позже для отображения списка эмодзи.

**src/компоненты/эмодзи-пикер.tsx**
````
import { Modal, View, Text, Pressable, StyleSheet } from 'react-native';
import { PropsWithChildren } from 'react';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = PropsWithChildren<{
  isVisible: boolean;
  onClose: () => void;
}>;

export default function EmojiPicker({ isVisible, children, onClose }: Props) {
  return (
    <View>
      <Modal animationType="slide" transparent={true} visible={isVisible}>
        <View style={styles.modalContent}>
          <View style={styles.titleContainer}>
            <Text style={styles.title}>Choose a sticker</Text>
            <Pressable onPress={onClose}>
              <MaterialIcons name="close" color="#fff" size={22} />
            </Pressable>
          </View>
          {children}
        </View>
      </Modal>
    </View>
  );
}

const styles = StyleSheet.create({
  modalContent: {
    height: '25%',
    width: '100%',
    backgroundColor: '#25292e',
    borderTopRightRadius: 18,
    borderTopLeftRadius: 18,
    position: 'absolute',
    bottom: 0,
  },
  titleContainer: {
    height: '16%',
    backgroundColor: '#464C55',
    borderTopRightRadius: 10,
    borderTopLeftRadius: 10,
    paddingHorizontal: 20,
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
  },
  title: {
    color: '#fff',
    fontSize: 16,
  },
});
````

Давайте узнаем, что делает вышеприведенный код:

* The <`Modal`> Компонент отображает заголовок и кнопку закрытия.
* Его `visible` реквизит принимает ценность `isVisible` и контролирует, открыт или закрыто модаль.
* Его `transparent` реквизит - это булевое значение, которое определяет, заполняет ли модаль весь вид.
* Его `animationType` реквизит определяет, как он входит и покидает экран. В этом случае он скользит из нижней части экрана.
* И, наконец, <`EmojiPicker`> Призывает onClose реквизит, когда пользователь нажимает на близкое <`Pressable`>.

Теперь давайте изменим `src/app/(tabs)/index.tsx` :

* Импортировать <`EmojiPicker`> компонент.
* Создать a isModalVisible переменная состояния с `useState` Крюк. Его значение по умолчанию является `false`, который скрывает модаль, пока пользователь не нажмет кнопку, чтобы открыть его.
* Заменить комментарий в `onAddSticker()` функция для обновления `isModalVisible` переменная для true когда пользователь нажимает кнопку. Это откроет сборщик смайликов.
* `isModalVisible` Переменная состояния.
* Поместите The <`EmojiPicker`> Компонент в нижней части `Index` компонент.

**src/app/(tabs)/index.tsx**
````
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';
import EmojiPicker from '@/components/emoji-picker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }

  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    setIsModalVisible(true);
  };

  const onModalClose = () => {
    setIsModalVisible(false);
  };

  const onSaveImageAsync = async () => {
    // we will implement this later
  };
````
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        {/* Emoji list component will go here */}
      </EmojiPicker>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
  optionsContainer: {
    position: 'absolute',
    bottom: 80,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
});
````

## Показать список смайликов
Давайте добавим горизонтальный список эмодзи в содержимое модала. Мы будем использовать <FlatList> Компонент от React Native для него.

Создайте файл `emoji-list.tsx` в каталоге `src/components` и добавьте следующий код:

**src/компоненты/эмодзи-лист.tsx**

````
import { useState } from 'react';
import { ImageSourcePropType, StyleSheet, FlatList, Platform, Pressable } from 'react-native';
import { Image } from 'expo-image';

type Props = {
  onSelect: (image: ImageSourcePropType) => void;
  onCloseModal: () => void;
};

export default function EmojiList({ onSelect, onCloseModal }: Props) {
  const [emoji] = useState<ImageSourcePropType[]>([
    require("@/assets/images/emoji1.png"),
    require("@/assets/images/emoji2.png"),
    require("@/assets/images/emoji3.png"),
    require("@/assets/images/emoji4.png"),
    require("@/assets/images/emoji5.png"),
    require("@/assets/images/emoji6.png"),
  ]);

  return (
    <FlatList
      horizontal
      showsHorizontalScrollIndicator={Platform.OS === 'web'}
      data={emoji}
      contentContainerStyle={styles.listContainer}
      renderItem={({ item, index }) => (
        <Pressable
          onPress={() => {
            onSelect(item);
            onCloseModal();
          }}>
          <Image source={item} key={index} style={styles.image} />
        </Pressable>
      )}
    />
  );
}

const styles = StyleSheet.create({
  listContainer: {
    borderTopRightRadius: 10,
    borderTopLeftRadius: 10,
    paddingHorizontal: 20,
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
  },
  image: {
    width: 100,
    height: 100,
    marginRight: 20,
  },
});
````

Давайте узнаем, что делает вышеприведенный код:

* The <`FlatList`> Компонент выше отображает все изображения эмодзи, используя Image компонент, обернутый a <`Pressable`>. Позже мы улучшим его, чтобы пользователь мог нажать смайлик на экране, чтобы он выглядел как наклейка на изображении.
* Он также принимает множество предметов, предоставленных emoji Переменная массива как значение data Прокв. The renderItem реквизит берет предмет из data и возвращает пункт в списке. Наконец, мы добавили Image и <`Pressable`> Компоненты для отображения этого элемента.
* The horizontal реквизит отображает список горизонтально, а не вертикально. The showsHorizontalScrollIndicator использует React Native's Platform модуль для проверки значения и отображения горизонтальной полосы прокрутки в Интернете.

Теперь обновите `src/app/(tabs)/index.tsx` Чтобы импортировать <`EmojiList`> компонент и замена комментариев внутри <`EmojiPicker`> компонент со следующим фрагментом кода:

**src/app/(tabs)/index.tsx**

````
import { ImageSourcePropType, View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';
import EmojiPicker from '@/components/emoji-picker';
import EmojiList from '@/components/emoji-list';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);
  const [pickedEmoji, setPickedEmoji] = useState<ImageSourcePropType | undefined>(undefined);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    setIsModalVisible(true);
  };

  const onModalClose = () => {
    setIsModalVisible(false);
  };

  const onSaveImageAsync = async () => {
    // we will implement this later
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        <EmojiList onSelect={setPickedEmoji} onCloseModal={onModalClose} />
      </EmojiPicker>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
  optionsContainer: {
    position: 'absolute',
    bottom: 80,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
});
````

В `EmojiList` компонент, `onSelect` реквизит выбирает эмодзи и после его выбора, `onCloseModal` Закрывает модаль.

## Отобразить выбранный emoji

Теперь мы поместим наклейку смайлика на изображение. Создайте новый файл в каталоге src/components и назовите его `emoji-sticker.tsx`. Затем добавьте следующий код:

**src/компоненты/эмодзи-стикер.tsx**
````
import { ImageSourcePropType, View } from 'react-native';
import { Image } from 'expo-image';

type Props = {
  imageSize: number;
  stickerSource: ImageSourcePropType;
};

export default function EmojiSticker({ imageSize, stickerSource }: Props) {
  return (
    <View style={{ top: -350 }}>
      <Image source={stickerSource} style={{ width: imageSize, height: imageSize }} />
    </View>
  );
}
````

Этот компонент получает два реквизита:

* imageSize: значение, определенное внутри `Index` компонент. Мы будем использовать это значение в следующей главе, чтобы масштабировать размер изображения при нажатии.
* stickerSource: Источник выбранного изображения эмодзи.

Импортировать этот компонент в `src/app/(tabs)/index.tsx `Файл и обновить Index компонент для отображения наклейки `emoji` на изображении. Мы проверим, `pickedEmoji` Государство не является `undefined`:

**src/app/(tabs)/index.tsx**
````
import { ImageSourcePropType, View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';
import EmojiPicker from '@/components/emoji-picker';
import EmojiList from '@/components/emoji-list';
import EmojiSticker from '@/components/emoji-sticker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);
  const [pickedEmoji, setPickedEmoji] = useState<ImageSourcePropType | undefined>(undefined);


  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    setIsModalVisible(true);
  };

  const onModalClose = () => {
    setIsModalVisible(false);
  };

  const onSaveImageAsync = async () => {
    // we will implement this later
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
        {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        <EmojiList onSelect={setPickedEmoji} onCloseModal={onModalClose} />
      </EmojiPicker>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
  optionsContainer: {
    position: 'absolute',
    bottom: 80,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
});
````
## Тема: Добавить жесты

**Жесты** - отличный способ обеспечить интуитивно понятный пользовательский опыт в приложении. Библиотека React Native Gesture Handler предоставляет встроенные нативные компоненты, которые могут обрабатывать жесты. Он распознает панорам, кран, вращение и другие жесты, используя нативную систему сенсорной обработки платформы. В этой главе мы добавим два разных жеста, используя эту библиотеку:

* Двойное нажатие, чтобы масштабировать размер наклейки `emoji` и уменьшить шкалу при двойном постукивании снова.
* Пан, чтобы переместить наклейку смайлика вокруг экрана, чтобы пользователь мог разместить наклейку в любом месте на изображении.

## Добавить ЖестОбработчикРужникПросмотр

Чтобы получить взаимодействие жестов для работы в приложении, мы вернемся <`GestureHandlerRootView`> от `react-native-gesture-handler` на вершине `Index` компонент. Заменить уровень корней <`View`> компонент в `src/app/(tabs)/index.tsx` с <`GestureHandlerRootView`>.

**src/app/(tabs)/index.tsx**

````
// ... rest of the import statements remain same
import { GestureHandlerRootView } from 'react-native-gesture-handler';

export default function Index() {
  return (
    <GestureHandlerRootView style={styles.container}>
      {/* ...rest of the code remains */}
    </GestureHandlerRootView>
  )
}
````

## Используйте анимированные компоненты

А `Animated` Компонент смотрит на `style` реквизит компонента и определяет, какие значения анимировать и применять обновления для создания анимации. Реанимированный экспорт анимированных компонентов, таких как <`Animated.View`>, <`Animated.Text`>, или <`Animated.ScrollView`>. Мы будем применять анимацию к <`Animated.Image`> компонент, чтобы сделать двойной жест нажатия работает.

* Откройте `emoji-sticker.tsx` Файл в `src/компоненты directory`. `Inside it`, `import Animated` от `react-native-reanimated` библиотека для использования анимированных компонентов.
* Replace the Image компонент с <`Animated.Image`>.

**src/компоненты/эмодзи-стикер.tsx**
````
import { ImageSourcePropType, View } from 'react-native';
import Animated from 'react-native-reanimated';

type Props = {
  imageSize: number;
  stickerSource: ImageSourcePropType;
};

export default function EmojiSticker({ imageSize, stickerSource }: Props) {
  return (
    <View style={{ top: -350 }}>
      <Animated.Image
        source={stickerSource}
        resizeMode="contain"
        style={{ width: imageSize, height: imageSize }}
      />
    </View>
  );
}
````
## Добавить жест нажатия

Добавить жест нажатия

`React Native Gesture Handler` позволяет нам добавлять поведение, когда он обнаруживает сенсорный ввод, например, двойное нажатие.

В `src/components/emioji-sticker.tsx` файле:

1. Импорт `Gesture` и `GestureDetector` от `react-native-gesture-handler`.
2. Чтобы распознать кран на наклейке, импортируйте `useAnimatedStyle`, useSharedValue, и withSpring от react-native-reanimated чтобы оживить стиль <Animated.Image>.
3. Внутри `EmojiSticker` компонент, создать ссылку, называемую scaleImage с помощью `useSharedValue()` Крюк. Это возьмет на себя ценность `imageSize` В качестве его первоначального значения.

**src/компоненты/эмодзи-стикер.tsx**

````
// ...rest of the import statements remain same
import { Gesture, GestureDetector } from 'react-native-gesture-handler';
import Animated, { useAnimatedStyle, useSharedValue, withSpring } from 'react-native-reanimated';

export default function EmojiSticker({ imageSize, stickerSource }: Props) {
  const scaleImage = useSharedValue(imageSize);

  return (
    // ...rest of the code remains same
  )
}
````
Создать следующий объект в EmojiSticker компонент:

**src/компоненты/эмодзи-стикер.tsx**
````
const doubleTap = Gesture.Tap()
  .numberOfTaps(2)
  .onStart(() => {
    if (scaleImage.value !== imageSize * 2) {
      scaleImage.value = scaleImage.value * 2;
    } else {
      scaleImage.value = Math.round(scaleImage.value / 2);
    }
  });
````

Создать a `imageStyle` переменная и добавить ее в `EmojiSticker` компонент:

**src/компоненты/эмодзи-стикер.tsx**
````
const imageStyle = useAnimatedStyle(() => {
  return {
    width: withSpring(scaleImage.value),
    height: withSpring(scaleImage.value),
  };
});
````
Далее, оберните <`Animated.Image`> Компонент с <`GestureDetector`> и изменить style Опора на <`Animated.Image`> чтобы пройти `imageStyle`.

**src/компоненты/эмодзи-стикер.tsx**
````
import { ImageSourcePropType, View } from 'react-native';
import { Gesture, GestureDetector } from 'react-native-gesture-handler';
import Animated, { useAnimatedStyle, useSharedValue, withSpring } from 'react-native-reanimated';

type Props = {
  imageSize: number;
  stickerSource: ImageSourcePropType;
};

export default function EmojiSticker({ imageSize, stickerSource }: Props) {
  const scaleImage = useSharedValue(imageSize);

  const doubleTap = Gesture.Tap()
    .numberOfTaps(2)
    .onStart(() => {
      if (scaleImage.value !== imageSize * 2) {
        scaleImage.value = scaleImage.value * 2;
      } else {
        scaleImage.value = Math.round(scaleImage.value / 2);
      }
    });

  const imageStyle = useAnimatedStyle(() => {
    return {
      width: withSpring(scaleImage.value),
      height: withSpring(scaleImage.value),
    };
  });

  return (
    <View style={{ top: -350 }}>
      <GestureDetector gesture={doubleTap}>
        <Animated.Image
          source={stickerSource}
          resizeMode="contain"
          style={[{ width: imageSize, height: imageSize }, imageStyle]}
        />
      </GestureDetector>
    </View>
  );
}
````

## Добавить жест сковороды

Чтобы распознать жест перетаскивания на наклейке и отследить ее движение, мы будем использовать жест сковороды. В `src/components/emoidji-sticker.tsx` :

1. Создайте две новые общие ценности: `translateX` и `translateY`.
2. Заменить <`View`> с <`Animated.View`> компонент.

**src/компоненты/эмодзи-стикер.tsx**
````
export default function EmojiSticker({ imageSize, stickerSource }: Props) {
  const scaleImage = useSharedValue(imageSize);
  const translateX = useSharedValue(0);
  const translateY = useSharedValue(0);
  // ...rest of the code remains same

  return (
    <Animated.View style={{ top: -350 }}>
      <GestureDetector gesture={doubleTap}>
        {/* ...rest of the code remains same */}
      </GestureDetector>
    </Animated.View>
  );
}
````
Давайте узнаем, что делает вышеприведенный код:

* Определенные значения перевода будут перемещать наклейку по экрану. Поскольку наклейка движется по обеим осям, нам нужно отслеживать значения `X` и `Y`.
* В `useSharedValue()` Крючки, мы установили обе переменные перевода, чтобы иметь начальную позицию 0. Это начальная позиция наклейки и отправная точка. Это значение устанавливает начальную позицию наклейки, когда начинается жест.

На предыдущем шаге мы спровоцировали `onStart()` обратный звонок для жеста крана, прикованного к `Gesture.Tap()` Метод. Для жеста сковороды укажите `onChange()` обратный звонок, который проходит, когда жест активен и движется.

1. Создать a `drag` объект, чтобы справиться с жестом сковороды. The `onChange()` обратный звонок принимает event в качестве параметра. `changeX` и `changeY` свойства удерживают изменение позиции с момента последнего события и обновляют значения, хранящиеся в `translateX` и `translateY`.
2. Определить `containerStyle` Объект, использующий `useAnimatedStyle()` Крюк. Это вернет множество преобразований. Для <`Animated.View`> компонент, нам нужно установить `transform` Имущество для `translateX` и `translateY` Ценности. Это изменит положение наклейки, когда жест активен.

## Тема: Сделать скриншот
## Установить библиотеки

Установить `react-native-view-shot` и `expo-media-library`, выполните следующие команды:
````
npx expo install react-native-view-shot expo-media-library
````
## Подсказка для разрешений

Добавьте следующий фрагмент кода внутрь `src/app/(tabs)/index.tsx`:

**src/app/(tabs)/index.tsx**
````
import { useEffect, useState } from 'react';
import * as ImagePicker from 'expo-image-picker';

// ...rest of the code remains same

export default function Index() {
  const [permissionResponse, requestPermission] = ImagePicker.useMediaLibraryPermissions();
  // ...rest of the code remains same

  useEffect(() => {
    if (!permissionResponse?.granted) {
      requestPermission();
    }
  }, []);

  // ...rest of the code remains same
}
````
## Создайте референт для сохранения текущего представления

Мы будем использовать `react-native-view-shot` чтобы позволить пользователю сделать снимок экрана в приложении. Эта библиотека захватывает скриншот <`View`> как изображение с использованием `captureRef()` Метод. Он возвращает `URI` захваченного файла снимков скриншота.

1. Импорт captureRef от `react-native-view-shot` и `useRef` От `React`.
2. Создать a `imageRef` эталонная переменная для хранения ссылки на снимок экрана, захваченного изображения.
3. Обернуть <`ImageViewer`> и <`EmojiSticker`> Компоненты внутри a <`View`> а затем передать ему справочную переменную.

**src/app/(tabs)/index.tsx**
````
import { useState, useRef } from 'react';
import { captureRef } from 'react-native-view-shot';

export default function Index() {
  const imageRef = useRef<View>(null);

  // ...rest of the code remains same

  return (
    <GestureHandlerRootView style={styles.container}>
      <View style={styles.imageContainer}>
        <View ref={imageRef} collapsable={false}>
          <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
          {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
        </View>
      </View>
      {/* ...rest of the code remains same */}
    </GestureHandlerRootView>
  );
}
````
## Снимите скриншот и сохраните его

Мы можем сделать скриншот вида, позвонив `captureRef()` Метод из `react-native-view-shot` внутри onSaveImageAsync() Функция. Он принимает факультативный аргумент, в котором мы можем пройти `width` и `height` область захвата скриншота. Мы можем прочитать больше о доступных вариантах в документация библиотеки.

The `captureRef()` Метод также возвращает обещание, которое выполняется с `URI` скриншота. Мы передадим этот `URI` в качестве параметра `MediaLibrary.saveToLibraryAsync()` и сохранить скриншот в медиатеку устройства.

Внутри `src/app/(tabs)/index.tsx`, обновить `onSaveImageAsync()` Функция со следующим кодом:

**src/app/(tabs)/index.tsx**
````
import * as ImagePicker from 'expo-image-picker';
import * as MediaLibrary from 'expo-media-library';
import { useEffect, useRef, useState } from 'react';
import { ImageSourcePropType, StyleSheet, View } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import { captureRef } from 'react-native-view-shot';

import Button from '@/components/button';
import CircleButton from '@/components/circle-button';
import EmojiList from '@/components/emoji-list';
import EmojiPicker from '@/components/emoji-picker';
import IconButton from '@/components/icon-button';
import ImageViewer from '@/components/image-viewer';

import EmojiSticker from '@/components/emoji-sticker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(
    undefined
  );
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);
  const [pickedEmoji, setPickedEmoji] = useState<
    ImageSourcePropType | undefined
  >(undefined);
  const [permissionResponse, requestPermission] = ImagePicker.useMediaLibraryPermissions();
  const imageRef = useRef<View>(null);

  useEffect(() => {
    if (!permissionResponse?.granted) {
      requestPermission();
    }
  }, []);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    setIsModalVisible(true);
  };

  const onModalClose = () => {
    setIsModalVisible(false);
  };

  const onSaveImageAsync = async () => {
    try {
      const localUri = await captureRef(imageRef, {
        height: 440,
        quality: 1,
      });

      await MediaLibrary.saveToLibraryAsync(localUri);
      if (localUri) {
        alert('Saved!');
      }
    } catch (e) {
      console.log(e);
    }
  };

  return (
    <GestureHandlerRootView style={styles.container}>
      <View style={styles.imageContainer}>
        <View ref={imageRef} collapsable={false}>
          <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
          {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
        </View>
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        <EmojiList onSelect={setPickedEmoji} onCloseModal={onModalClose} />
      </EmojiPicker>
    </GestureHandlerRootView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
  optionsContainer: {
    position: 'absolute',
    bottom: 80,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
});
````
## Тема: Обработка различий платформы
## Установить и импортировать dom-to-image

Чтобы запечатлеть снимок экрана в Интернете и сохранить его в качестве изображения, мы будем использовать стороннюю библиотеку под названием `dom-to-image`. Он берет скриншот любого узла DOM и превращает его в векторный (`SVG`) или растровый (`PNG` или `JPEG`) изображение.

Остановите сервер разработки и выполните следующую команду для установки библиотеки:
````
npm install dom-to-image
````
## Добавить код, специфичный для платформы

Использовать `Platform` модуль от React Native, мы можем реализовать платформу специфическое поведение. Внутри `src/app/(tabs)/index.tsx`:

1.Импортировать `Platform` Модуль от `react-native`.
2. Импортировать `domtoimage` библиотека от `dom-to-image`.
3. Обновить `onSaveImageAsync()` функция, чтобы проверить, является ли текущая платформа '`web`' с `Platform.OS` собственность. Если это так '`web`', мы будем использовать `domtoimage.toJpeg()` способ преобразования и захвата тока <`View`> В качестве изображения `JPEG`. В противном случае мы будем продолжать использовать ту же логику, добавленную для собственных платформ.

**src/app/(tabs)/index.tsx**
````
import * as ImagePicker from 'expo-image-picker';
import * as MediaLibrary from 'expo-media-library';
import { useEffect, useRef, useState } from 'react';
import { ImageSourcePropType, View, StyleSheet, Platform } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import { captureRef } from 'react-native-view-shot';
import domtoimage from 'dom-to-image';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';
import EmojiPicker from '@/components/emoji-picker';
import EmojiList from '@/components/emoji-list';
import EmojiSticker from '@/components/emoji-sticker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);
  const [pickedEmoji, setPickedEmoji] = useState<ImageSourcePropType | undefined>(undefined);
  const [permissionResponse, requestPermission] = ImagePicker.useMediaLibraryPermissions();
  const imageRef = useRef<View>(null);

  useEffect(() => {
    if (!permissionResponse?.granted) {
      requestPermission();
    }
  }, []);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => {
    setShowAppOptions(false);
  };

  const onAddSticker = () => {
    setIsModalVisible(true);
  };

  const onModalClose = () => {
    setIsModalVisible(false);
  };

  const onSaveImageAsync = async () => {
    if (Platform.OS !== 'web') {
      try {
        const localUri = await captureRef(imageRef, {
          height: 440,
          quality: 1,
        });

        await MediaLibrary.saveToLibraryAsync(localUri);
        if (localUri) {
          alert('Saved!');
        }
      } catch (e) {
        console.log(e);
      }
    } else {
      try {
        const dataUrl = await domtoimage.toJpeg(imageRef.current, {
          quality: 0.95,
          width: 320,
          height: 440,
        });

        let link = document.createElement('a');
        link.download = 'sticker-smash.jpeg';
        link.href = dataUrl;
        link.click();
      } catch (e) {
        console.log(e);
      }
    }
  };

  return (
    <GestureHandlerRootView style={styles.container}>
      <View style={styles.imageContainer}>
        <View ref={imageRef} collapsable={false}>
          <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
          {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
        </View>
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        <EmojiList onSelect={setPickedEmoji} onCloseModal={onModalClose} />
      </EmojiPicker>
    </GestureHandlerRootView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
  optionsContainer: {
    position: 'absolute',
    bottom: 80,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
});
````
## Тема: Настройка панели состояния, экрана брызг и значка приложения
## Настройка строки состояния

Внутри `src/app/_layout.tsx` :

1. Импорт `StatusBar` от `expo-status-bar`.
2. Группа The `StatusBar` и существующих `Stack` компоненты с Компонент Фрагмента `React`.

**src/app/_layout.tsx**
````
import { Stack } from 'expo-router';
import { StatusBar } from 'expo-status-bar';

export default function RootLayout() {
  return (
    <>
      <Stack>
        <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
      </Stack>
      <StatusBar style="light" />
    </>
  );
}
````

## Иконка приложения

Внутри проекта есть файл icon.png внутри каталога активов/изображений. Это иконка нашего приложения.
Иконка приложения

Внутри проекта есть файл icon.png внутри каталога активов/изображений. Это иконка нашего приложения. Это изображение 1024px на 1024px и выглядит так, как показано ниже:
Значок приложения по умолчанию: темный округлый квадрат, показывающий белый фотоглиф с желтым смайликом.

Как и изображение всплеска экрана, "icon" собственность в app.json файл настраивает путь значка приложения. По умолчанию новый проект Expo определяет правильный путь "./assets/images/icon.png". Нам не нужно ничего менять.
 
## Всплеск экрана

Экран брызг виден до загрузки контента приложения. Он использует меньший образ, такой как значок приложения, который центрирован. Он скрывается, как только контент приложения готов к отображению.

The `expo-splash-screen` Плагин уже поставляется предустановленным в каждом созданном проекте `create-expo-app`. Эта библиотека предоставляет плагин конфигурирования для настройки экрана брызг.

В `app.json`, `expo-splash-screen` плагин уже настроен на использование значка приложения в качестве изображения экрана брызг (предоставлено в загружаемые активы) со следующим фрагментом, поэтому нам не нужно ничего менять:

**app.json**

````
{
  "plugins": [
    ... 
    [
      "expo-splash-screen",
      {
        "image": "./assets/images/splash-icon.png"
        ... 
      }
    ]
  ]
}
````
## Тема: Учебные ресурсы
## Создайте свой проект в приложение

Чтобы начать создавать новое приложение на вашей машине, вы можете использовать `npx create-expo-app@latest` и Настройте свою среду разработки последовательно.
Рекомендуемые ресурсы

После того, как вы создали свой новый проект, вы можете узнать больше о различных инструментах и концепциях, которые помогут вам в вашем путешествии по разработке приложения:

* Инструменты разработки: Справка инструментов `Expo`, которые помогут вам во время различных аспектов вашего путешествия по созданию приложений.
* Разработка: Использование сборки разработки позволяет вам получить полный контроль над процессом сборки вашего приложения и тестировать ваше приложение на устройстве или симуляторе.
* Обзор развития: Это обзор высокого уровня, в котором содержится подробная информация о ключевых концепциях разработки приложения с `Expo` и потоке петли развития ядра.
* Expo Router : Мы прошли через основы `Expo` Router и реализовали навигатор вкладки. Смотрите его документацию, чтобы узнать больше о библиотеке.
* Значок приложения и экран брызг: Вы можете узнать больше о настройке значка приложения и руководства по брызгам экрана. Кроме того, проверьте ссылку на настройки приложения для свойств, которые вы можете настроить в файл `app.json`.
* Распространение и представление приложений в магазины приложений: прочитайте эти ресурсы, чтобы узнать больше о том, как выпустить и отправить свое приложение в магазины приложений, как только оно будет готово к отправке.
* DebuggingОтладка: иногда что-то идет не так, и когда они это делают, вы можете использовать инструменты отладки, чтобы найти и исправить ошибки.

## Обучение
**Реагировать**

Мы использовали компоненты React и API. Наличие твердого понимания React имеет важное значение для использования Expo для создания вашего приложения. Мы рекомендуем прочитать раздел «Быстрый старт» документации React и раздел «Крючки».

**React Native**

При разработке учебного приложения мы широко использовали `React Native`. Вы можете начать с руководства по основам `React Native`, чтобы узнать больше. Кроме того, проверьте следующие документы:

* Просмотр API Reference
* Текст API ссылка
* Платформа специфический код
* Представление данных в списке

Мы использовали Flexbox для компоновки наших компонентов. Ознакомьтесь со следующими рекомендациями, чтобы узнать больше об этом:

* Высота и ширина
* Макет с помощью Flexbox

**Жесты и анимация**

Чтобы узнать больше о внедрении различных типов жестов и анимации, мы рекомендуем следующую документацию:

* Реагировать Нативный Жест Обработчик
* React Native Reanimated






## Тема: ЗНАКОМСТВО С `JavaScript`

## тема: Введение в `JavaScript`

## Что такое `JavaScript`?
Изначально `JavaScript` был создан, чтобы «сделать веб-страницы живыми».

Программы на этом языке называются скриптами. Они могут встраиваться в `HTML` и выполняться автоматически при загрузке веб-страницы.

Скрипты распространяются и выполняются, как простой текст. Им не нужна специальная подготовка или компиляция для запуска.

Это отличает ``JavaScript`` от другого языка – ``Java``.
Сегодня JavaScript может выполняться не только в браузере, но и на сервере или на любом другом устройстве, которое имеет специальную программу, называющуюся «движком» JavaScript.

У браузера есть собственный движок, который иногда называют «виртуальная машина `JavaScript`».

Разные движки имеют разные «кодовые имена». Например:

`V8 – в Chrome, Opera и Edge`.
`SpiderMonkey – в Firefox.`
…Ещё есть «`Chakra`» для IE, «`JavaScriptCore`», «`Nitro`» и «`SquirrelFish`» для Safari и т.д.

Эти названия полезно знать, так как они часто используются в статьях для разработчиков. Мы тоже будем их использовать. Например, если «функциональность `X` поддерживается `V8`», тогда «`Х`», скорее всего, работает в Chrome, Opera и Edge.

Движки сложны. Но основы понять легко.

1. Движок (встроенный, если это браузер) читает («парсит») текст скрипта.
2. Затем он преобразует («компилирует») скрипт в машинный язык.
3. После этого машинный код запускается и работает достаточно быстро.

Движок применяет оптимизации на каждом этапе. Он даже просматривает скомпилированный скрипт во время его работы, анализируя проходящие через него данные, и применяет оптимизации к машинному коду, полагаясь на полученные знания. В результате скрипты работают очень быстро.

## Что может JavaScript в браузере?
Современный JavaScript – это «безопасный» язык программирования. Он не предоставляет низкоуровневый доступ к памяти или процессору, потому что изначально был создан для браузеров, не требующих этого.

Возможности JavaScript сильно зависят от окружения, в котором он работает. Например, Node.js поддерживает функции чтения/записи произвольных файлов, выполнения сетевых запросов и т.д.

В браузере для JavaScript доступно всё, что связано с манипулированием веб-страницами, взаимодействием с пользователем и веб-сервером.

Например, в браузере JavaScript может:

* Добавлять новый HTML-код на страницу, изменять существующее содержимое, модифицировать стили.
* Реагировать на действия пользователя, щелчки мыши, перемещения указателя, нажатия клавиш.
* Отправлять сетевые запросы на удалённые сервера, скачивать и загружать файлы (технологии AJAX и COMET).
* Получать и устанавливать куки, задавать вопросы посетителю, показывать сообщения.
* Запоминать данные на стороне клиента («local storage»).

## Чего НЕ может JavaScript в браузере? 
Возможности JavaScript в браузере ограничены ради безопасности пользователя. Цель заключается в предотвращении доступа недобросовестной веб-страницы к личной информации или нанесения ущерба данным пользователя.

Примеры таких ограничений включают в себя:

* JavaScript на веб-странице не может читать/записывать произвольные файлы на жёстком диске, копировать их или запускать программы. Он не имеет прямого доступа к системным функциям ОС.
Современные браузеры позволяют ему работать с файлами, но с ограниченным доступом, и предоставляют его, только если пользователь выполняет определённые действия, такие как «перетаскивание» файла в окно браузера или его выбор с помощью тега <`input`>.

* Различные окна/вкладки не знают друг о друге. Иногда одно окно, используя JavaScript, открывает другое окно. Но даже в этом случае JavaScript с одной страницы не имеет доступа к другой, если они пришли с разных сайтов (с другого домена, протокола или порта).
Это называется «Политика одинакового источника» (Same Origin Policy). Чтобы обойти это ограничение, обе страницы должны согласиться с этим и содержать JavaScript-код, который специальным образом обменивается данными.

* JavaScript может легко взаимодействовать с сервером, с которого пришла текущая страница. Но его способность получать данные с других сайтов/доменов ограничена. Хотя это возможно в принципе, для чего требуется явное согласие (выраженное в заголовках `HTTP`) с удалённой стороной. Опять же, это ограничение безопасности.

## Что делает JavaScript особенным?
Как минимум, три сильные стороны JavaScript:

Полная интеграция с `HTML/CSS`.
Простые вещи делаются просто.
Поддерживается всеми основными браузерами и включён по умолчанию.

**JavaScript** – это единственная браузерная технология, сочетающая в себе все эти три вещи.

Вот что делает JavaScript особенным. Вот почему это самый распространённый инструмент для создания интерфейсов в браузере.

Хотя, конечно, JavaScript позволяет делать приложения не только в браузерах, но и на сервере, на мобильных устройствах и т.п.

## Языки «над» JavaScript

Синтаксис JavaScript подходит не под все нужды. Разные люди хотят иметь разные возможности.

Это естественно, потому что проекты разные и требования к ним тоже разные.

Так, в последнее время появилось много новых языков, которые транспилируются (конвертируются) в JavaScript, прежде чем запустятся в браузере.

Современные инструменты делают транспиляцию очень быстрой и прозрачной, фактически позволяя разработчикам писать код на другом языке, автоматически преобразуя его в JavaScript «под капотом».

Примеры таких языков:

* `CoffeeScript` добавляет «синтаксический сахар» для JavaScript. Он вводит более короткий синтаксис, который позволяет писать чистый и лаконичный код. Обычно такое нравится Ruby-программистам.
* `TypeScript` концентрируется на добавлении «строгой типизации» для упрощения разработки и поддержки больших и сложных систем. Разработан Microsoft.
* `Flow` тоже добавляет типизацию, но иначе. Разработан Facebook.
* `Dart` стоит особняком, потому что имеет собственный движок, работающий вне браузера (например, в мобильных приложениях). Первоначально был предложен Google, как замена JavaScript, но на данный момент необходима его транспиляция для запуска так же, как для вышеперечисленных языков.
* `Brython` транспилирует Python в JavaScript, что позволяет писать приложения на чистом Python без JavaScript.


Есть и другие. Но даже если мы используем один из этих языков, мы должны знать JavaScript, чтобы действительно понимать, что мы делаем.

## Тема: Справочники и спецификации
## Спецификация

Спецификация ECMA-262 содержит самую глубокую, детальную и формализованную информацию о JavaScript. Она определяет сам язык.

Вначале спецификация может показаться тяжеловатой для понимания из-за слишком формального стиля изложения. Если вы ищете источник самой достоверной информации, то это правильное место, но она не для ежедневного использования.

Новая версия спецификации появляется каждый год. А пока она не вышла официально, все желающие могут ознакомиться с текущим черновиком на `https://tc39.es/ecma262/`.

Чтобы почитать о самых последних возможностях, включая те, которые «почти в стандарте» (так называемые «stage 3 proposals»), посетите `https://github.com/tc39/proposals`.

Если вы разрабатываете под браузеры, то существуют и другие спецификации, о которых рассказывается во второй части этого учебника.

## Справочники
MDN (Mozilla) JavaScript Reference – это справочник с примерами и другой информацией. Хороший источник для получения подробных сведений о функциях языка, методах встроенных объектов и так далее.

Располагается по адресу `https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference`.

Хотя зачастую вместо их сайта удобнее использовать какой-нибудь интернет-поисковик, вводя там запрос «MDN [что вы хотите найти]», например `https://google.com/search?q=MDN+parseInt` для поиска информации о функции parseInt.

## Таблицы совместимости
**JavaScript** – это развивающийся язык, в который постоянно добавляется что-то новое.

Посмотреть, какие возможности поддерживаются в разных браузерах и других движках, можно в следующих источниках:

* `https://caniuse.com` – таблицы с информацией о поддержке по каждой возможности языка. Например, чтобы узнать, какие движки поддерживают современные криптографические функции, посетите: `https://caniuse.com/#feat=cryptography`.
* `https://kangax.github.io/compat-table` – таблица с возможностями языка и движками, которые их поддерживают и не поддерживают.
Все эти ресурсы полезны в ежедневной работе программиста, так как они содержат ценную информацию о возможностях использования языка, их поддержке и так далее.

Пожалуйста, запомните эти ссылки (или ссылку на эту страницу) на случай, когда вам понадобится подробная информация о какой-нибудь конкретной возможности JavaScript.

## Тема: Редакторы кода
## IDE

Термином `IDE` (Integrated Development Environment, «интегрированная среда разработки») называют мощные редакторы с множеством функций, которые работают в рамках целого проекта. Как видно из названия, это не просто редактор, а нечто большее.

`IDE` загружает проект (который может состоять из множества файлов), позволяет переключаться между файлами, предлагает автодополнение по коду всего проекта (а не только открытого файла), также она интегрирована с системой контроля версий (например, такой как git), средой для тестирования и другими инструментами на уровне всего проекта.

Если вы ещё не выбрали себе `IDE`, присмотритесь к этим:

* **Visual Studio Code** (кросс-платформенная, бесплатная).
WebStorm (кросс-платформенная, бесплатная для некоммерческого использования).
Для Windows есть ещё Visual Studio (не путать с Visual Studio Code). 
*  **Visual Studio** – это платная мощная среда разработки, которая работает только на Windows. Она хорошо подходит для .NET платформы. У неё есть бесплатная версия, которая называется **Visual Studio Community**.

Многие `IDE` платные, но у них есть пробный период. Их цена обычно незначительна по сравнению с зарплатой квалифицированного разработчика, так что пробуйте и выбирайте ту, что вам подходит лучше других.

## «Лёгкие» редакторы
«Лёгкие» редакторы менее мощные, чем `IDE`, но они отличаются скоростью, удобным интерфейсом и простотой.

В основном их используют для того, чтобы быстро открыть и отредактировать нужный файл.

Главное отличие между «лёгким» редактором и `IDE` состоит в том, что `IDE` работает на уровне целого проекта, поэтому она загружает больше данных при запуске, анализирует структуру проекта, если это необходимо, и так далее. Если вы работаете только с одним файлом, то гораздо быстрее открыть его в «лёгком» редакторе.

На практике «лёгкие» редакторы могут иметь множество плагинов, включая автодополнение и анализаторы синтаксиса на уровне директории, поэтому границы между `IDE` и «лёгкими» редакторами размыты.

Следующие варианты заслуживают вашего внимания:

Sublime Text (кроссплатформенный, условно-бесплатный).
Notepad++ (Windows, бесплатный).
Vim и Emacs тоже хороши, если знать, как ими пользоваться.

## Тема: Консоль разработчика

Код уязвим для ошибок. И вы, скорее всего, будете делать ошибки в коде… Впрочем, давайте будем откровенны: вы точно будете совершать ошибки в коде. В конце концов, вы человек, а не робот.

Но по умолчанию в браузере ошибки не видны. То есть, если что-то пойдёт не так, мы не увидим, что именно сломалось, и не сможем это починить.

Для решения задач такого рода в браузер встроены так называемые «Инструменты разработки» (Developer tools или сокращённо — `devtools`).

Код уязвим для ошибок. И вы, скорее всего, будете делать ошибки в коде… Впрочем, давайте будем откровенны: вы точно будете совершать ошибки в коде. В конце концов, вы человек, а не робот.

Но по умолчанию в браузере ошибки не видны. То есть, если что-то пойдёт не так, мы не увидим, что именно сломалось, и не сможем это починить.

Для решения задач такого рода в браузер встроены так называемые «Инструменты разработки» (Developer tools или сокращённо — devtools).

## Google Chrome
В её JavaScript-коде закралась ошибка. Она не видна обычному посетителю, поэтому давайте найдём её при помощи инструментов разработки.

Нажмите F12 или, если вы используете Mac, Cmd+Opt+J.

По умолчанию в инструментах разработчика откроется вкладка Console (консоль).

Точный внешний вид инструментов разработки зависит от используемой версии Chrome. Время от времени некоторые детали изменяются, но в целом внешний вид остаётся примерно похожим на предыдущие версии.

В консоли мы можем увидеть сообщение об ошибке, отрисованное красным цветом. В нашем случае скрипт содержит неизвестную команду `«lalala»`.
Справа присутствует ссылка на исходный код `bug.html:12` с номером строки кода, в которой эта ошибка и произошла.
Под сообщением об ошибке находится синий символ `>`. Он обозначает командную строку, в ней мы можем редактировать и запускать JavaScript-команды. Для их запуска нажмите Enter.

## Firefox, Edge и другие

Инструменты разработчика в большинстве браузеров открываются при нажатии на F12.

Их внешний вид и принципы работы мало чем отличаются. Разобравшись с инструментами в одном браузере, вы без труда сможете работать с ними и в другом.

## Safari

Safari (браузер для Mac, не поддерживается в системах Windows/Linux) всё же имеет небольшое отличие. Для начала работы нам нужно включить «Меню разработки» («Developer menu»).

## Тема: Основы JavaScript

## Привет, мир!
**Тег «script»**
````
<!DOCTYPE HTML>
<html>

<body>

  <p>Перед скриптом...</p>

  <script>
    alert( 'Привет, мир!' );
  </script>

  <p>...После скрипта.</p>

</body>

</html>
````

## Тема: Структура кода
## Инструкции

**Инструкции** – это синтаксические конструкции и команды, которые выполняют действия.

Мы уже видели инструкцию alert(`'Привет, мир!'`), которая отображает сообщение «`Привет, мир!`».

В нашем коде может быть столько инструкций, сколько мы захотим. Инструкции могут отделяться точкой с запятой.

Например, здесь мы разделили сообщение «Привет Мир» на два вызова alert:

````
alert(`'Привет'`); 
alert(`'Мир'`);
````

Обычно каждую инструкцию пишут на новой строке, чтобы код было легче читать:

````
alert(`'Привет'`);
alert(`'Мир'`);
````

## Точка с запятой
В большинстве случаев точку с запятой можно не ставить, если есть переход на новую строку.

Так тоже будет работать:

```
alert('Привет')

alert('Мир')
````

## Комментарии
Со временем программы становятся всё сложнее и сложнее. Возникает необходимость добавлять комментарии, которые бы описывали, что делает код и почему.

Комментарии могут находиться в любом месте скрипта. Они не влияют на его выполнение, поскольку движок просто игнорирует их.

Однострочные комментарии начинаются с двойной косой черты `//`.

Часть строки после `//` считается комментарием. Такой комментарий может как занимать строку целиком, так и находиться после инструкции.

Как здесь:
````
// Этот комментарий занимает всю строку
alert('Привет');

alert('Мир'); // Этот комментарий следует за инструкцией
````

## Тема: Строгий режим — "use strict"

На протяжении долгого времени JavaScript развивался без проблем с обратной совместимостью. Новые функции добавлялись в язык, в то время как старая функциональность не менялась.

Преимуществом данного подхода было то, что существующий код продолжал работать. А недостатком – что любая ошибка или несовершенное решение, принятое создателями JavaScript, застревали в языке навсегда.

Так было до 2009 года, когда появился ECMAScript 5 (ES5). Он добавил новые возможности в язык и изменил некоторые из существующих. Чтобы устаревший код работал, как и раньше, по умолчанию подобные изменения не применяются. Поэтому нам нужно явно их активировать с помощью специальной директивы: "`use strict`".

### «use strict»
Директива выглядит как строка: "`use strict`" или '`use strict`'. Когда она находится в начале скрипта, весь сценарий работает в «современном» режиме.

Например:
````
"use strict";
// этот код работает в современном режиме
...
````

Совсем скоро мы начнём изучать функции (способ группировки команд), поэтому заранее отметим, что в начале большинства видов функций можно поставить "`use strict`". Это позволяет включить строгий режим только в конкретной функции. Но обычно люди используют его для всего файла.

Переменные
JavaScript-приложению обычно нужно работать с информацией. Например:

Интернет-магазин – информация может включать продаваемые товары и корзину покупок.
Чат – информация может включать пользователей, сообщения и многое другое.
Переменные используются для хранения этой информации.

## Тема: Переменная
**Переменная** – это «именованное хранилище» для данных. Мы можем использовать переменные для хранения товаров, посетителей и других данных.

Для создания переменной в JavaScript используйте ключевое слово `let`.

Приведённая ниже инструкция создаёт (другими словами, объявляет) переменную с именем `«message»`:
````
let message;
````
Теперь можно поместить в неё данные (другими словами, определить переменную), используя оператор присваивания =:
````
let message;

message = 'Hello'; // сохранить строку 'Hello' в переменной с именем message
````
Строка сохраняется в области памяти, связанной с переменной. Мы можем получить к ней доступ, используя имя переменной:
````
let message;
message = 'Hello!';

alert(message); // показывает содержимое переменной
````
Для краткости можно совместить объявление переменной и запись данных в одну строку:
````
let message = 'Hello!'; // определяем переменную и присваиваем ей значение

alert(message); // Hello!
````

Мы также можем объявить несколько переменных в одной строке:

let user = 'John', age = 25, message = 'Hello';
Такой способ может показаться короче, но мы не рекомендуем его. Для лучшей читаемости объявляйте каждую переменную на новой строке.

Многострочный вариант немного длиннее, но легче для чтения:
````
let user = 'John';
let age = 25;
let message = 'Hello';
````
Некоторые люди также определяют несколько переменных в таком вот многострочном стиле:
````
let user = 'John',
  age = 25,
  message = 'Hello';
  ````
…Или даже с запятой в начале строки:
````
let user = 'John'
  , age = 25
  , message = 'Hello';
  ````
В принципе, все эти варианты работают одинаково. Так что это вопрос личного вкуса и эстетики.

## Тема: Типы данных

Переменная в JavaScript может содержать любые данные. В один момент там может быть строка, а в другой – число:
````
// Не будет ошибкой
let message = "hello";
message = 123456;
````
## Число
````
let n = 123;
n = 12.345;
````
## BigInt
В JavaScript тип number не может безопасно работать с числами, большими, чем (253-1) (т. е. 9007199254740991) или меньшими, чем -(253-1) для отрицательных чисел.

Если говорить совсем точно, то, технически, тип number может хранить большие целые числа (до 1.7976931348623157 * 10308), но за пределами безопасного диапазона целых чисел ±(253-1) будет ошибка точности, так как не все цифры помещаются в фиксированную 64-битную память. Поэтому можно хранить «приблизительное» значение.

Например, эти два числа (прямо за пределами безопасного диапазона) совпадают:
````
console.log(9007199254740991 + 1); // 9007199254740992
console.log(9007199254740991 + 2); // 9007199254740992
````

Строка
Строка (string) в JavaScript должна быть заключена в кавычки.
````
let str = "Привет";
let str2 = 'Одинарные кавычки тоже подойдут';
let phrase = `Обратные кавычки позволяют встраивать переменные ${str}`;
````
В JavaScript существует три типа кавычек.

1. Двойные кавычки: "Привет".
2. Одинарные кавычки: 'Привет'.
3. Обратные кавычки: `Привет`.

содержать ноль символов (быть пустой), один символ или множество.

## Булевый (логический) тип
Булевый тип (boolean) может принимать только два значения: true (истина) и false (ложь).

Такой тип, как правило, используется для хранения значений да/нет: true значит «да, правильно», а false значит «нет, не правильно».

Например:
````
let nameFieldChecked = true; // да, поле отмечено
let ageFieldChecked = false; // нет, поле не отмечено
````
Булевые значения также могут быть результатом сравнений:
````
let isGreater = 4 > 1;

alert( isGreater ); // true (результатом сравнения будет "да")
````

## Тема: Взаимодействие: alert, prompt, confirm

##alert
С этой функцией мы уже знакомы. Она показывает сообщение и ждёт, пока пользователь нажмёт кнопку «ОК».

Например:
````
alert("Hello");
````
## prompt
Функция prompt принимает два аргумента:
````
result = prompt(title, [default]);
Этот код отобразит модальное окно с текстом, полем для ввода текста и кнопками OK/Отмена.
````
`title`

Текст для отображения в окне.

`default`

Необязательный второй параметр, который устанавливает начальное значение в поле для текста в окне.

## confirm
Синтаксис:
````
result = confirm(question);
````
Функция confirm отображает модальное окно с текстом вопроса question и двумя кнопками: `OK и Отмена`.

Результат – `true`, если нажата кнопка `OK`. В других случаях – `false`.

Например:
````
let isBoss = confirm("Ты здесь главный?");

alert( isBoss ); // true, если нажата OK
````
Итого
Мы рассмотрели 3 функции браузера для взаимодействия с пользователем:

`alert`

показывает сообщение.

`prompt`

показывает сообщение и запрашивает ввод текста от пользователя. Возвращает напечатанный в поле ввода текст или `null`, если была нажата кнопка `«Отмена»` или `Esc` с клавиатуры.

`confirm`

показывает сообщение и ждёт, пока пользователь нажмёт `OK` или Отмена. Возвращает true, если нажата `OK`, и `false`, если нажата кнопка «Отмена» или `Esc` с клавиатуры.
Все эти методы являются модальными: останавливают выполнение скриптов и не позволяют пользователю взаимодействовать с остальной частью страницы до тех пор, пока окно не будет закрыто.

На все указанные методы распространяются два ограничения:

1. Расположение окон определяется браузером. Обычно окна находятся в центре.
2. Визуальное отображение окон зависит от браузера, и мы не можем изменить их вид.