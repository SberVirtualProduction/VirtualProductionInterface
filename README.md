## VirtualProductionInterface

Данный плагин содержит файл конфигурации сетапа для позиционирования сцены. А так же другие материалы обеспечивающие взаимодействие с системой NDisplay во время мероприятий.

Весь контент должен находиться в подпапке(например Content/MyGame/…) Это помогает в миграции между проектами и разделении контента графического и пакетов NDisplay.

# Что не используем в Virtual Production
Ultra Dynamic Sky

# Работа со слоями
## Добавление в AR слой</summary>
- Переходим в окно Edit->Project Settings...
- Находим параметр Depth-Stencil Pass(Engine->Rendering->Postprocessing->Custom Depth-Stencil Pass) и задаем значение <b>"Enabled with Stencil"</b>
- В объекте,который хотим перенести в ar слой, для всех Static mesh меняем следующие параметры:
  - Rendering->Render CustomDepth Pass = <b>enable</b>
  - Rendering->CustomDepth Stencil Value = <b>1</b>

## Удаление из слоя экрана</summary>
Добавитьте выбранные объекты к слою <b>VPStudio|LedIgnore</b>

# Обязательно в Post process
Чтобы подготовить нашу сцену к действительно линейному рабочему цветовому пространству, сделайте следующее:
- Создайте том постобработки (PPV) и установите для него значение Infinite Extend (Unbound).
- Нормализуйте экспозицию сцены, установив следующие параметры в разделе «Exposure» PPV.
- Metering Mode установлен на «Auto Exposure Histogram»
- Exposure Compensation установлен на 1,0
- Min EV100 установлен на 1,0
- Max EV100 также установлен на 1,0

Отключите следующие функции цветокоррекции в разделе Color Grading -> Misc, установив для них значение 0,0:
- Blue Correction
- Expand Gamut
- Tone Curve Amount

Отключите некоторые эффекты объектива, влияющие на цвет, установив для них значение 0,0:
- Vignette Intensity
- Bloom -> Intensity
- Lens Flares


# Render target
Плагин содержит render target (./Content/Material/RT_InputImage.uasset), который можно использовать для отображения статических слайдов презентации в процессе мероприятия.

![RT_InputImage.uasset](/docs/RenderTarget.png)
</details>

# NDI

Возможно использовать передачу изображения по сети, для это нужно установить NDI(все 3), доступно по [ссылке](https://drive.google.com/drive/folders/1LPjtdLZqGwoN8tVWBuq9wtrwLebodtgI?usp=share_link).

Затем скопировать папку c плагином нужной версии (для 4.27 по умолчанию C:\Program Files\NDI\NDI SDK for Unreal Engine\PluginBuilds\UE_4.27\NDIIO) в папку с плагинами внутри проекта (папка Plugins в основной папке с проектом). 

После этого можно использовать файл Content\Material\MT_InputVideo.uasset внутри материалов для вывода полученного по сети видео.

# Точка ноль сцены и анимация пролета

Используйте Blueprints\BP_NDC_Axes для задания точки ноль сцены, а так же можете анимировать этот объект для создания пролетов по сцене.

# Event

Сетевые ивенты получаются через delagate DisplayClusterClusterEventInt, доступ к которому можно получить через EventComponent прикрепленный к актеру. Для избежания путаницы используйте event в диапазоне 0-100

![EventComponent](/docs/AddEventComponent.png)

![DisplayClusterClusterEvent](/docs/Delegate.png)

![UseDelagate](/docs/UseEvent.png)

## License

[MIT](https://choosealicense.com/licenses/mit/)