## VirtualProductionInterface

Данный плагин содержит файл конфигурации сетапа для позиционирования сцены. А так же другие материалы обеспечивающие взаимодействие с системой NDisplay во время мероприятий.

Весь контент должен находиться в подпапке(например Content/MyGame/…) Это помогает в миграции между проектами и разделении контента графического и пакетов NDisplay.

## Что не используем в Virtual Production

Ultra Dynamic Sky

## В Post process используем:
* Bloom.Intensity = 0
* Vignette.Intensity = 0
* Blue correction = 0
* Expand Gamut = 0
* Tone Curve Amount = 0

## Render target

Плагин содержит render target (./Content/Material/RT_InputImage.uasset), который можно использовать внутри контента в случаях, когда содержимое должно меняться в процессе мероприятия.

![RT_InputImage.uasset](/docs/RenderTarget.png)

## Event

Сетевые ивенты получаются через delagate DisplayClusterClusterEvent, доступ к которому можно получить через EventComponent прикрепленный к актеру. Для избежания путаницы используйте event в диапазоне 0-100

![EventComponent](/docs/AddEventComponent.png)

![DisplayClusterClusterEvent](/docs/Delegate.png)

![UseDelagate](/docs/UseEvent.png)
