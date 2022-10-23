+++
title = "Загрузка/Обновление мода"
description = ""
weight = 5
+++

## Подготовка вашего модуля для публикации

Вам необходимо опубликовать свой модуль через набор инструментов для моддинга, чтобы позволить другим игрокам использовать ваш модуль. Вы можете развернуть его для конечного пользователя, выделенных серверов или других моддеров, все это описано ниже.

### Экспорт модуля через Modding Tools

* Откройте Modding Kit через Launcher после проверки вашего мода в списке модулей Launcher`а.
* Откройте редактор через главное меню
* В верхнем меню File выберите Publish Module

![](/img/uploading_updating_mod/1.png)

Во всплывающем окне Publishing доступны следующие параметры:

|                                        |                                        |
|----------------------------------------|----------------------------------------|
| ![](/img/uploading_updating_mod/2.png) | ![](/img/uploading_updating_mod/3.png) |

* `Client`: Ваш модуль будет упакован для использования клиентом. Это означает, что игрокам потребуются эти пакеты, чтобы играть в игру. Это минимальное, что вам нужно сделать, если вы хотите, чтобы ваш модуль воспроизводился через Steam Workshop.
* `Dedicated Server`: Ваш модуль также может быть запущен на сервере. Если вы хотите, чтобы ваш мод был доступен и в многопользовательской игре, вам нужно проверить это.
* `Editor`: Другие игроки могут открыть ваш модуль через редактор и изменить его. Если вы не упакуете для редактора, игроки не смогут открыть ваш модуль через редактор.

{{% notice warning %}}
Do not forget to select your module in the “Module” dropdown list. Otherwise, you will most likely publish the Native module by accident which will take a significant amount of time.
{{% /notice %}}

* После выбора этих параметров и вашего модуля в раскрывающемся списке «Modules» нажмите кнопку «Publish».
* После нажатия кнопки «Publish» появится всплывающее окно для выбора каталога назначения. Выберите целевой каталог, доступный для записи на вашем компьютере, и модуль будет скопирован туда как готовая к загрузке версия.
* Затем просто загрузите папку мода в папку назначения в Steam Workshop, следуя инструкциям, указанным в разделах «**Создание нового предмета Мастерской Steam**» и «**Обновление предмета Мастерской Steam**».

{{% notice warning %}}
If you, as a modder, are going to test your module after uploading to the Steam Workshop, please temporarily move your Module folder under “Steam\steamapps\common\Mount & Blade II Bannerlord\Modules” to somewhere else. If you don’t move it temporarily, then the game will try to fetch the module from Bannerlord/Modules instead of workshop/content/261550.
{{% /notice %}}

## Creating a new Steam Workshop Item

### Подготовка WorkshopCreate.xml

Download [this file](https://download.taleworlds.com/WorkshopCreate.xml) and place it anywhere you want. You can also create one with the following code:

```xml
<Tasks>
    <CreateItem/>
    <UpdateItem>
        <ModuleFolder Value="C:\Program Files (x86)\Steam\steamapps\common\Mount &amp; Blade II Bannerlord\Modules\YourModuleName"/>
        <!-- A direct path of your module -->
        <ItemDescription Value="A Bannerlord Mod"/>
        <!-- A description that will be displayed on Steam Workshop, can be edited via the Steam UI -->
        <Tags>
            <!-- You can use the following tags: -->
            <!-- Type: Graphical Enhancement, Map Pack, Partial Conversion, Sound, Total Conversion, Troops, UI, Utility, Weapons and Armour -->
            <!-- Setting: Native, Antiquity, Dark Ages, Medieval, Musket Era, Modern, Sci-Fi, Fantasy, Oriental, Apocalypse, Other -->
            <!-- Game Mode: Singleplayer, Multiplayer -->
            <!-- Compatible Version: e1.9.0, v1.0.0,... The currently available versions can be found at the Steam Workshop "Browse by Tag" section -->
            <Tag Value="Partial Conversion" />
            <Tag Value="Dark Ages" />
            <Tag Value="Singleplayer" />
            <Tag Value="Multiplayer" />
            <Tag Value="e1.9.0" />
        </Tags>
        <Image Value="C:\Program Files (x86)\Steam\steamapps\common\Mount &amp; Blade II Bannerlord\Modules\YourModuleName\Image.png"/>
        <!-- Determines the featured image displayed on Steam Workshop, a direct path to it must be inserted here (the image should be smaller than 1 MB) -->
        <Visibility Value="Public"/>
        <!-- Determines visibility on Steam Workshop. Can be: Public, FriendsOnly, Private -->
    </UpdateItem>
</Tasks>
```

* Open the file using Notepad, Notepad++ or other tools
* Edit the `Items` to match your module
    * `ModuleFolder`: A direct path of your module
    * `ItemDescription`: A description that will be displayed on Steam Workshop, can be edited via the Steam UI
    * `Tags`: Allows your mod to be found by filtering categories. Here are the tags you can assign to your item:
        * `Type`: Graphical Enhancement, Map Pack, Partial Conversion, Sound, Total Conversion, Troops, UI, Utility, Weapons and Armour
        * `Setting`: Native, Antiquity, Dark Ages, Medieval, Musket Era, Modern, Sci-Fi, Fantasy, Oriental, Apocalypse, Other
        * `Game Mode`: Singleplayer, Multiplayer
        * `Compatible Version`: e1.9.0, v1.0.0,... (the currently available versions can be found at the Steam Workshop "Browse by Tag" section)
        * You’re encouraged to only use the above tags as they’re what players will be able to filter mods by. Any other tags won’t show up on the Filter list but will show up on your mod Steam Workshop page
    * `Image`: Determines the featured image displayed on Steam Workshop, a direct path to it must be inserted here (the image should be smaller than 1 MB)
    * `Visibility`: Determines visibility on Steam Workshop. Can be: Public, FriendsOnly, Private
* Save the changes made to `WorkshopCreate.xml`

{{% notice warning %}}
Steam Cloud must be enabled for the game in order to successfully upload your mod. You can verify that by right-clicking on Mount &amp; Blade II: Bannerlord within your Steam Library, going to Properties and then General. Or by enabling Steam Cloud for all games via the Steam client Settings window, via the Cloud tab.
{{% /notice %}}

{{% notice warning %}}
You may run into an error during the publishing process. An endless print of the following line: Status: k_EItemUpdateStatusInvalid 0/0 - If that occurs your upload may have completed successfully and you’re free to close the console. If the upload failed, try again.
{{% /notice %}}

{{% notice tip %}}
The size of your uploaded module displayed on the Steam Workshop may differ from the actual size of the module. This is normal.
{{% /notice %}}

### Публикация модуля
* Find the following folder `\Steam\steamapps\common\Mount & Blade II Bannerlord\bin\Win64_Shipping_Client` and confirm that the `TaleWorlds.MountAndBlade.SteamWorkshop.exe` is located inside of it
* Type `cmd` into the bar where the folder location is displayed and press `Enter`
* Type `TaleWorlds.MountAndBlade.SteamWorkshop.exe c:\path\WorkshopCreate.xml` into the console, with the path directing to your `WorkshopCreate.xml` file and press `Enter`
* If no errors appear, your mod has been successfully uploaded to Steam Workshop

## Updating a Steam Workshop Item

### Подготовка WorkshopUpdate.xml

Download [this file](https://download.taleworlds.com/WorkshopUpdate.xml) and place it anywhere you want. You can also create one with the following code:

```xml
<Tasks>
    <GetItem>
        <ItemId Value="YourWorkshopItemIdHere"/>
        <!-- Can be found in the URL of your workshop item -->
    </GetItem>
    <UpdateItem>
        <ModuleFolder Value="C:\Mount &amp; Blade II Bannerlord\Modules\MyMod"/>
        <!-- A direct path of your module -->	
        <ChangeNotes Value="New cool features" />
        <!-- Insert patch notes -->
        <Tags> 
            <!-- You can use the following tags: -->
            <!-- Type: Graphical Enhancement, Map Pack, Partial Conversion, Sound, Total Conversion, Troops, UI, Utility, Weapons and Armour -->
            <!-- Setting: Native, Antiquity, Dark Ages, Medieval, Musket Era, Modern, Sci-Fi, Fantasy, Oriental, Apocalypse, Other -->
            <!-- Game Mode: Singleplayer, Multiplayer -->
            <!-- Compatible Version: e1.9.0, v1.0.0,... The currently available versions can be found at the Steam Workshop "Browse by Tag" section -->
            <Tag Value="Partial Conversion" />
            <Tag Value="Dark Ages" />
            <Tag Value="Singleplayer" />
            <Tag Value="Multiplayer" />
            <Tag Value="e1.9.0" />
        </Tags>
    </UpdateItem>
</Tasks>
```

* Open the file using Notepad, Notepad++ or other tools
* Edit the `Items` to match your module
    * `ItemId`: Insert the ID of your workshop module. You can find it by going to your workshop module page, right-clicking on a blank slot and selecting `Copy Page URL`. If you then paste the URL somewhere, you’ll see the ID.
    * `ModuleFolder`: A direct path of your module
    * `ChangeNotes`: Think of this as patch notes, they will be displayed on the “Change Notes” section of your Workshop module
    * `Tags`: Allows your mod to be found by filtering categories. Updating tags can be done through the `WorkshopUpdate.xml` file
* Save the changes made to `WorkshopUpdate.xml`

### Публикация обновления
* Find the following folder `\Steam\steamapps\common\Mount & Blade II Bannerlord\bin\Win64_Shipping_Client` and confirm that the `TaleWorlds.MountAndBlade.SteamWorkshop.exe` is located inside of it
* Type `cmd` into the bar where the folder location is displayed and press `Enter`
* Type `TaleWorlds.MountAndBlade.SteamWorkshop.exe c:\path\WorkshopUpdate.xml` into the console, with the path directing to your `WorkshopUpdate.xml` file and press `Enter`
* If no errors appear, your mod has been successfully updated