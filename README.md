## VirtualProductionInterface

Данный плагин содержит файл конфигурации сетапа для позиционирования сцены. А так же другие материалы обеспечивающие взаимодействие с системой NDisplay во время мероприятий.

Весь контент должен находиться в подпапке(например Content/MyGame/…) Это помогает в миграции между проектами и разделении контента графического и пакетов NDisplay.

<details><summary>Что не используем в Virtual Production</summary>
    * Ultra Dynamic Sky
</details>
- asd
<P><details><summary>Работа со слоями</summary>
    <blockquote>
        <details><summary>Добавление в AR слой</summary>
            <blockquote>
                Переходим в окно Edit->Project Settings...
                - Находим параметр Depth-Stencil Pass(Engine->Rendering->Postprocessing->Custom Depth-Stencil Pass) и задаем значение **"Enabled with Stencil"**
                В объекте Static mesh, в который хотим перенести в ar слой, меняем следующие параметры:
                - Rendering->Render CustomDepth Pass = **enable**
                - Rendering->CustomDepth Stencil Value = **1**
                <P>
            </blockquote>
        </details>
        <details><summary>Удаление из слоя экрана</summary>
            <blockquote>
                Добавитьте выбранные объекты к слою **VPStudio|LedIgnore**
            </blockquote>
        </details>
    </blockquote>
</details>

<details><summary>Обязательно в Post process</summary>
    <P>Чтобы подготовить нашу сцену к действительно линейному рабочему цветовому пространству, сделайте следующее:
    Создайте том постобработки (PPV) и установите для него значение Infinite Extend (Unbound).
    <P>Нормализуйте экспозицию сцены, установив следующие параметры в разделе «Exposure» PPV.
    <P>* Metering Mode установлен на «Auto Exposure Histogram»
    <P>* Exposure Compensation установлен на 1,0
    <P>* Min EV100 установлен на 1,0
    <P>* Max EV100 также установлен на 1,0
    <P>Отключите следующие функции цветокоррекции в разделе Color Grading -> Misc, установив для них значение 0,0:
    <P>* Blue Correction
    <P>* Expand Gamut
    <P>* Tone Curve Amount
    <P>Отключите некоторые эффекты объектива, влияющие на цвет, установив для них значение 0,0:
    <P>* Vignette Intensity
    <P>* Bloom -> Intensity
    <P>* Lens Flares
</details>


<details><summary>Render target</summary>

Плагин содержит render target (./Content/Material/RT_InputImage.uasset), который можно использовать для отображения статических слайдов презентации в процессе мероприятия.

![RT_InputImage.uasset](/docs/RenderTarget.png)
</details>

<details><summary>NDI</summary>

Возможно использовать передачу изображения по сети, для это нужно установить NDI(все 3), доступно по [ссылке](https://drive.google.com/drive/folders/1LPjtdLZqGwoN8tVWBuq9wtrwLebodtgI?usp=share_link).

Затем скопировать папку c плагином нужной версии (для 4.27 по умолчанию C:\Program Files\NDI\NDI SDK for Unreal Engine\PluginBuilds\UE_4.27\NDIIO) в папку с плагинами внутри проекта (папка Plugins в основной папке с проектом). 

После этого можно использовать файл Content\Material\MT_InputVideo.uasset внутри материалов для вывода полученного по сети видео.
</details>

<details><summary>Event</summary>

Сетевые ивенты получаются через delagate DisplayClusterClusterEventInt, доступ к которому можно получить через EventComponent прикрепленный к актеру. Для избежания путаницы используйте event в диапазоне 0-100

![EventComponent](/docs/AddEventComponent.png)

![DisplayClusterClusterEvent](/docs/Delegate.png)

![UseDelagate](/docs/UseEvent.png)
</details>