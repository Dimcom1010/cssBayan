# cssBayan
## Вы можете взглянуть на мой проект по ссылке
## [_Bayan_](https://dimcom1010.github.io/cssBayan/cssBayan/index.html)

### С вашего позволения хочу немного рассказать про свой проект.
####Давай сперва разберём HTLM файл, а затем перейдём к стилям 
 ##  head
```
<head>
    <meta charset="UTF-8">  //Указываем кодировку документа
    <meta http-equiv="X-UA-Compatible" content="IE=edge">//  Директива X-UA-Compatible призывает Internet Explorer работать в определённом режиме документа.
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> // Meta-тег viewport сообщает браузеру о том, как именно обрабатывать размеры страницы
    <title>cssBayan</title> //   заголовок сайта
    <link rel="shortcut icon" href="src/img/favicon-32x32.png" type="image/x-icon"> // подключение favicon (это иконка в левой стороны от title)

    <link rel="preconnect" href="https://fonts.googleapis.com"> 
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Lato:wght@400;700;900&display=swap" rel="stylesheet">
//  подключение шрифтов с сайта https://fonts.google.com/

    <link rel="stylesheet" href="reset.css"> // подключение файла css с обнуляющими параметрами.
    <link rel="stylesheet" href="style.css"> // подключение файла css с основными стилями страницы
</head>
```

 ##  body

```
<body>
    Блок wrapper отвечает за задний  
    <div class="wrapper"> 

        Блок container отвечает за область за пределы которой не будет выходить наш баян, и весь остальной контент который мы хотель бы отобразить на нашей странице
        <div class="container">
            Блок bayan_wrapper отвечает за расположение баян в контейнере, вложенность может от части показаться излишней, но это лишь потому что мы на странице отображаем только лишь баян, если бы у нас были ещё элементы такие как заглавие футеры   ещё какой-нибудь контент, такая структура помогла бы нам просто управлять позиционирования каждого элемента в контейнере.  
            <div class="bayan_wrapper">
            
                Блок bayan_item это один элемент раскрывающегося меню он состоит тэга  <label> привязанного с 
                <input> типа  «radio» при помощи атрибута «for» 
                <label class="bayan_item" for="bayan_1">

                    <input> типа «radio»  имеет атрибут " name="bayan" по этому атрибуту мы можем объединять множество input в группу в таком случае при нажатии на один input он помечается как “checked» а и этот атрибут автоматически убирается у input которые был активный до нажатия. В верстке мы его не видем так как он спрятан стилями по своё поведение он передаёт всему тэгу label
                     <input class="bayan_input" type="radio" name="bayan" id="bayan_1">

	            Блок bayan_label содержит название вкладки и крестик
                    <div class="bayan_label">
                        <div class="lable_text">When you have completed all the tasks</div>
                        <div class="lable_cross">+</div>
                    </div>

                    Блок bayan_content содержит мем
                    <div class="bayan_content">
                        <img src="src/img/mem_13.jpg" alt="mem_1">
                    </div>
                </label>
                ***
                Ещё 4 блока .bayan_item
                *** 	
            </div>
        </div>
    </div>
</body>
```




#### Стили css не буду останавливать на каждом но на некоторых задержусь

псевдокласс :root находит корневой элемент в дом дереве. Используем его что бы объявить переменные для нашего css 
/переменные я разделил на категории 
_цвета_
```
/* color variables*/
:root{
  --bg: #ffffff;
  --bg_bayan: #ffffff;
  --bg_lable: #8486CA;
  --bg_lable_active: #505294;
  --text_lable: #494a6fc5;
  --text_lable_active: 	#171847;
}
```
_анимация_
```
/* animation variables*/
:root{
  --animation_style: 0.9s cubic-bezier(0.075, 0.82, 0.165, 1);
}
```
_адаптивность_
```
/* adiptiv variables*/
:root{
  --distop: 1200;
  --min_text_size: 10px;
  --deff_text_size: 13;
  --width_img:50%;
}
```
В коде ниже вы увидите, что не для всех свойств я испольховал переменные, а лиш для тех которые наибоее часто повторяются и которые мне нужны били  

В body устанавливаю общие стили для всего документа, тут это только тип шрифта
```
/* styles cssBayan*/
body{
  font-family: 'Lato', sans-serif;
}
```
Задний фон занимает всю площадь экрана 
```
.wrapper{
  width: 100%;
  min-height: 100vw;
  background: var(--bg);
  overflow: hidden;
}
```

Ширина контейнера рассчитывается исходя из шириды экрана пользователя  формула расчёта следующая Тут [^1]

``` 
.container{
  width: calc(200px + 400 * (100vw / var(--distop)));
  margin: 20px auto;
  max-width: 500px;
}
```
Проявление креста я сделал при помощи _opacity_ оно меняется со значения 0 до 1 
```
.bayan_wrapper:hover .lable_cross{
  opacity: 1;
  justify-content: end;
}


.bayan_wrapper:hover .bayan_label{
  color: var(--text_lable_active);
}

.bayan_item{
  display: flex;
  flex-direction: column;
  width: 100%;
  align-items: center;
  background: var(--bg_bayan);
  border: 1px solid var(--bg_lable_active);
  cursor: pointer;
  border-radius: 5px;
}
```
appearance используется для управления внешним видом , что бы отключить стили _input_ которые у него по умолчанию по умолчанию , устанавливаем  _appearance_: none; для того что бы спрятать _input_ устанавливаем 
```
.bayan_input{
  height: 0;
  width: 0;
  margin: 0;
  appearance: none;
}
```
Когда у input активирован у него появляется атрибут _checked_ и превдокласс  _:checked_, в этом случае мы при помощи ~ ищем класс .bayan_content, который находится на томже уровне вложенности что и _input_ и меняем классу _.bayan_ параметр  _display_ с _«none»_ на  _«flex»_
```
.bayan_input:checked ~ .bayan_content{
  display: flex;
}
```
"+" позволяет обратиться к следующиму за _.bayan_input:checked_ элементу  + _.bayan_label_
```
.bayan_input:checked + .bayan_label{
  color: var(--text_lable_active);
}
```
Если _input_ активирован ищем на томже уровне вложенности класс _.bayan_label_ и обращаемся к его дочернему элементу с классом _.lable_cross_ и устанавливаем ему _transform: rotateZ(405deg)_; про число 405 и вращение можно почитать в сноске [^2]

```
.bayan_input:checked ~ .bayan_label > .lable_cross{
  transform: rotateZ(405deg);
}

.bayan_input:checked ~ .bayan_content img,
.bayan_input:hover ~ .bayan_content img,
.bayan_content:hover > img{
  display: flex;
  width: var(--width_img);
}

.bayan_input:hover ~ .bayan_content{
  display: flex;
}
```
про transform и загадочное 405deg смотри выше [^2]
.bayan_input:hover ~ .bayan_label > .lable_cross{
  transform: rotateZ(405deg);
}


 _font-size_ рассчитываю динамически, также как и ширину контейнера разбор формулы тут [^1]
 _cursor: pointer;_ меняет курсор руку с тальцем.
 ```
.bayan_label{
  background: var(--bg_lable);
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 10px 20px;
  font-size: calc(
    var(--min_text_size) + var(--deff_text_size) * (100vw / var(--distop))
);
  transition: var(--animation_style);
  color: var(--text_lable);
  cursor: pointer;
}

.bayan_label:hover {
  background: var(--bg_lable_active);
}
.bayan_label:hover > .lable_text {
  color: var(--bg);
}

.lable_text{
  transition: var(--animation_style);
  max-width: 95%;
}

.lable_cross{
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 900;
  transition: var(--animation_style);
  opacity: 0;
}
```

 Плавное появление картинки я реализовал при помощи анимации _«size»_ она проигрывается один раз при появлении картинки 
 ```
.bayan_content img{
  display: none;
  width: 0;
  margin: 0px auto;
  animation: 0.7s ease-in running size;
}
```
При наведении на мем курсор меняется на какртинку favicon если картинку не нашёл используется курсор по умолчанию _стрелочка_
```
img:hover{
  cursor: url(src/img/favicon-32x32.png), default;
}
```

Этот медиа запрос помогает остановить увеличение текста при достижении экрана ширины более _1200рх_ 
```
@media (min-width: 1200px) {
  .bayan_label{
    font-size: 23px;
  }
}
```

Ключевые кадры анимации , увеличение размера картинки от 0 до размера указанного  в переменной --width_img 
```
@keyframes size {
  from {
    width: 0%;
  }
  to {
    width: var(--width_img);
  }
}
```



 [^1]:вращает крестик много раз ,  для того что бы из «+» получить «х» нужно повернуть его на _45 градусов_,  но что бы было интереснее я _45 * 9 = 405_ и таким образом он вращается.  _calc( размер контейнера при минимальном разрешении + количество пикселей которое мы будем прибавлять к этому числу в процессе расширения экрана до максимального , максимальное значение экрана лежит в переменной   --distop и равно 1200px  )_. Это необходимо для плавного изменения размера контейнера при изменениях размера экрана, такую же формулу я использую и для шрифта. 

 [^2]:вращает крестик много раз ,  для того что бы из «+» получить «х» нужно повернуть его на _45 градусов_,  но что бы было интереснее я _45 * 9 = 405_ и таким образом он вращается.