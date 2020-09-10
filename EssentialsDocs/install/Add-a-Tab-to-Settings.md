---
title: Добавление вкладки в раздел "Параметры"
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: aac6b7f3-9020-46c3-a83f-b81542300385
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 17f2d7c8a409ed49ea0f9bfa50952467e4694243
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623990"
---
# <a name="add-a-tab-to-settings"></a>Добавление вкладки в раздел "Параметры"

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Для добавления вкладки в раздел Параметры на панели мониторинга нужно создать и установить сборку кода, используемую диспетчером параметров операционной системы.

## <a name="add-a-tab-to-settings"></a>Добавить вкладку в Параметры
 Чтобы добавить вкладку в параметры, нужно выполнить следующие действия:

-   [Добавление в сборку реализации интерфейса ISettingsData](Add-a-Tab-to-Settings.md#BKMK_ISettingsData).

-   [Поставьте на сборке подпись Authenticode](Add-a-Tab-to-Settings.md#BKMK_SignAssembly).

-   [Установка сборки на компьютере-образце](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly).

###  <a name="add-an-implementation-of-the-isettingsdata-interface-to-the-assembly"></a><a name="BKMK_ISettingsData"></a> Добавление в сборку реализации интерфейса Исеттингсдата
 Интерфейс ISettingsData включен в пространство имен Microsoft.WindowsServerSolutions.Settings сборки AdminCommon.dll, которая расположена в папке \Program Files\Windows Server\Bin.

##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>Добавление в сборку реализации интерфейса ISettingsData

1.  Откройте Visual Studio 2010 с правами администратора, щелкнув эту программу правой кнопкой мыши в меню **Пуск** и выбрав команду **Запуск от имени администратора**.

2.  В меню **Файл** выберите команду **Создать** и щелкните пункт **Проект**.

3.  В диалоговом окне **Новый проект** последовательно щелкните **Visual C#**, затем **Библиотека классов**, введите **DashboardSettingsPage** в качестве имени решения и нажмите кнопку **OK**.

    > [!IMPORTANT]
    >  Сборку, устанавливаемую на сервер, необходимо назвать DashboardSettingsPage.dll и затем скопировать DLL в папку %ProgramFiles%\Windows Server\Bin\OEM.

4.  Создайте элемент управления, который будет использоваться на вкладке. В этом примере элемент управления "Параметры" называется Мисеттингсконтрол.

5.  Присвойте файлу Class1.cs другое имя, например MySettingTab.cs.

6.  Добавьте ссылку на файл AdminCommon.dll.

7.  Добавьте следующую инструкцию using:

    ```c#
    using Microsoft.WindowsServerSolutions.Settings;
    ```

8.  Измените пространство имен и заголовок класса аналогично следующему примеру:

    ```

    namespace DashboardSettingsPage
    {
        public class MySettingTab : ISettingsData
        {
        }
    }

    ```

9. Создайте экземпляр элемента управления, созданного для вкладки. Например:

    ```c#
    private MySettingsControl tab;
    ```

10. Добавьте конструктор для класса. Подобный конструктор показан в следующем примере кода:

    ```

    public MySettingTab()
    {
       tab = new MySettingsControl();
    }
    ```

11. Добавьте метод Commit, который отправляет изменения параметров. Метод Commit показан в следующем примере кода:

    ```

    void ISettingsData.Commit(bool dismissed)
    {
       // Implement the code that is required to submit your setting changes
    }
    ```

12. Добавьте метод TabControl, определяющий элемент управления для вкладки. В следующем примере кода показан метод TabControl:

    ```

    System.Windows.Forms.Control ISettingsData.TabControl
    {
       get { return tab; }
    }
    ```

13. Добавьте метод Табид, который предоставляет уникальный идентификатор для вкладки. В следующем примере кода показан метод Табид:

    ```

    private Guid id = Guid.NewGuid();

    Guid ISettingsData.TabId
    {
       get { return id; }
    }
    ```

14. Добавьте метод Табордер, который возвращает порядок вкладки. В следующем примере кода показан метод Табордер:

    ```

    int ISettingsData.TabOrder
    {
       get { return 0; }
    }
    ```

    > [!NOTE]
    >  Порядковый номер вкладки отсчитывается от 0. Сначала отображаются встроенные вкладки параметров Майкрософт, а пользовательские вкладки отображаются в соответствии с указанными для них порядковыми номерами. Например, при наличии трех вкладок параметров для них указываются порядковые номера 0, 1 и 2 в соответствии с порядком отображения вкладок.

15. Добавьте метод Табтитле, который предоставляет заголовок вкладки. В следующем примере кода показан метод Табтитле:

    ```

    string ISettingsData.TabTitle
    {
      get { return "My Settings Tab"; }
    }
    ```

    > [!NOTE]
    >  При необходимости локализации программного обеспечения для предоставления заголовка вкладки можно также использовать файл ресурсов.

16. Сохраните решение и выполните его построение.

###  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a> Подписать сборку с помощью подписи Authenticode
 Чтобы сборку можно было использовать в операционной системе, на ней должна быть подпись Authenticode. Дополнительные сведения о подписи сборки см. в разделе [Подпись и проверка кода с помощью Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).

###  <a name="install-the-assembly-on-the-reference-computer"></a><a name="BKMK_InstallAssembly"></a> Установка сборки на эталонном компьютере
 В случае успешного построения решения поместите копию файла DashboardSettingsPage.dll в следующую папку на компьютере-образце:

 **%Programfiles%\Windows Server\Bin\OEM**

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)