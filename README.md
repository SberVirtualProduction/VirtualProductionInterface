## VirtualProductionInterface

Данный плагин содержит файл конфигурации сетапа для позиционирования сцены. А так же другие материалы обеспечивающие взаимодействие с системой NDisplay во время мероприятий.

Весь контент должен находиться в подпапке(например Content/MyGame/…) Это помогает в миграции между проектами и разделении контента графического и пакетов NDisplay.

## Что не используем в Virtual Production

Ultra Dynamic Sky

## В Post process используем:
Чтобы подготовить нашу сцену к действительно линейному рабочему цветовому пространству, сделайте следующее:

Создайте том постобработки (PPV) и установите для него значение Infinite Extend (Unbound).
Нормализуйте экспозицию сцены, установив следующие параметры в разделе «Exposure» PPV.
* Metering Mode установлен на «Auto Exposure Histogram»
* Exposure Compensation установлен на 1,0
* Min EV100 установлен на 1,0
* Max EV100 также установлен на 1,0

Отключите следующие функции цветокоррекции в разделе Color Grading -> Misc, установив для них значение 0,0:
* Blue Correction
* Expand Gamut
* Tone Curve Amount


Отключите некоторые эффекты объектива, влияющие на цвет, установив для них значение 0,0:

* Vignette Intensity
* Bloom -> Intensity
* Lens Flares

## Render target

Плагин содержит render target (./Content/Material/RT_InputImage.uasset), который можно использовать внутри контента в случаях, когда содержимое должно меняться в процессе мероприятия.

![RT_InputImage.uasset](/docs/RenderTarget.png)

## Event

Сетевые ивенты получаются через delagate DisplayClusterClusterEvent, доступ к которому можно получить через EventComponent прикрепленный к актеру. Для избежания путаницы используйте event в диапазоне 0-100

![EventComponent](/docs/AddEventComponent.png)

![DisplayClusterClusterEvent](/docs/Delegate.png)

![UseDelagate](/docs/UseEvent.png)
