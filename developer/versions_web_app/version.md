# Perform web application versioning

> Версионирование веб-приложений может регулироваться различными системами и методологиями. 
> Однако, подход, основанный на формате `major.minor.maintenance`, является довольно распространенным и легко понятным.
Вот общие рекомендации по использованию данного формата версионирования:
 - `Major (главная версия)`: Инкрементируется, когда вносятся существенные изменения или добавляются новые функциональные возможности (новые бизнес требования), которые могут повлиять на обратную совместимость. Например, обновление до главной версии 2.0 может включать полное перепроектирование интерфейса или изменение архитектуры приложения.
 - `Minor (минорная версия)`: Инкрементируется, когда добавляются новые бизнес функции или улучшения, но они не нарушают обратную совместимость с предыдущими версиями. Обычно это включает исправления ошибок, добавление новых модулей или обновление существующих функций. Например, обновление до минорной версии 1.2 может добавить новый фильтр или улучшить производительность приложения.
 - `Maintenance (версия исправления или patch)`: Инкрементируется при внесении исправлений ошибок или патчей без добавления новой функциональности или изменения обратной совместимости. Обычно это включает исправление критических ошибок без изменения основной функциональности приложения. Например, исправление версии 1.2.1 может устранить проблему с авторизацией или обновить сторонние библиотеки.

P.S
- Если совместимые изменения с предыдущей версией, то поднимаем `минорную версию`, если нет, то `мажорную`.
- Если `минорную` версию поднимаем, то версионность по исправлениям скидывается до 0. То есть должно быть 4.13.0, вместо 4.12.123.
- Если `мажорную` поднимаем, то скидываются всё (и минор и исправления) 5.0.0 вместо 4.12.123.