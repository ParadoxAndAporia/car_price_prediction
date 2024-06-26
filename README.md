# Прогнозирование цен на автомобили
<h1>Содержание<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#Прогнозирование-цен-на-автомобили" data-toc-modified-id="Прогнозирование-цен-на-автомобили-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>Прогнозирование цен на автомобили</a></span><ul class="toc-item"><li><span><a href="#Описание-проекта" data-toc-modified-id="Описание-проекта-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>Описание проекта</a></span></li><li><span><a href="#Описание-данных" data-toc-modified-id="Описание-данных-1.2"><span class="toc-item-num">1.2&nbsp;&nbsp;</span>Описание данных</a></span></li><li><span><a href="#Вывод" data-toc-modified-id="Вывод-1.3"><span class="toc-item-num">1.3&nbsp;&nbsp;</span>Вывод</a></span></li></ul></li></ul></div>
 
## Описание проекта
Сервис по продаже автомобилей с пробегом «Не бит, не крашен» разрабатывает приложение для привлечения новых клиентов. В нём можно быстро узнать рыночную стоимость своего автомобиля. В моем распоряжении исторические данные: технические характеристики, комплектации и цены автомобилей. Мне нужно построить модель для определения стоимости.
Заказчику важны:
- качество предсказания;
- скорость предсказания;
- время обучения.


## Описание данных

- DateCrawled — дата скачивания анкеты из базы
- VehicleType — тип автомобильного кузова
- RegistrationYear — год регистрации автомобиля
- Gearbox — тип коробки передач
- Power — мощность (л. с.)
- Model — модель автомобиля
- Kilometer — пробег (км)
- RegistrationMonth — месяц регистрации автомобиля
- FuelType — тип топлива
- Brand — марка автомобиля
- NotRepaired — была машина в ремонте или нет
- DateCreated — дата создания анкеты
- NumberOfPictures — количество фотографий автомобиля
- PostalCode — почтовый индекс владельца анкеты (пользователя)
- LastSeen — дата последней активности пользователя
- Price — цена (евро)
 
## Вывод
Исходя из полученных результатов можно сделать вывод, что: 
- CatBoost: среднеквадратичная ошибка - 1319.15, на тренировку данной модели ушло 5min 37
- Случайный лес: тренеруется очень долго, fit time в 159.65, что в ~ 30 раз выше, чем у LightGBM 4.78, при этом метрика best_score - 0.881, что чуть лучше, чем у LightGBG - 0.878, в силу чего RMSE у случайного леса - 1539.61.
- LightGBM: RMSE - 1583.45, на тренировку ушло 21.1s c. 
<br>

- RMSE моделей CatBoost и LightGBM почти совпадают, но CatBoost тренировался быстрее всех. (если смотреть без времени затраченного на подбор оптимальных параметров для CatBoost)
<br>

Согласно поставленным условиям, решающим факторами при выборе модели являются следующие показатели:

- Время обучения
- Время предсказания
- Качество предсказаний
<br>
Таким образом, если для наших задач важнее всего время - наш выбор - LightGMB, она обходит CatBoost по двум критериям из трех.
Однако, если нужна точность - лучше заряжать CatBoost. 
<br>
- **И победителем объявляется: LightGMB!**
