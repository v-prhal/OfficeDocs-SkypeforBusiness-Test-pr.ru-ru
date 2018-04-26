﻿---
title: Просмотр сведений о политике PIN-кода
TOCTitle: Просмотр сведений о политике PIN-кода
ms:assetid: 1d48b060-d77f-44ee-b70f-3ce128aedac4
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ687985(v=OCS.15)
ms:contentKeyID: 49887889
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Просмотр сведений о политике PIN-кода

 

_**Дата изменения раздела:** 2013-02-23_

Вкладка **Политика ПИН-кода** используется для просмотра данных о проверке подлинности с использованием персонального идентификационного номера (ПИН-кода) для пользователей, подключающихся к Lync 2013 с помощью IP-телефона. Чтобы использовать проверку подлинности по ПИН-коду, необходимо установить флажок **Включить проверку подлинности по ПИН-коду** в настройках веб-службы. Дополнительные сведения см. в разделе [Изменение параметров конфигурации существующей веб-службы](lync-server-2013-modify-existing-web-service-configuration-settings.md).

Чтобы изменить политику ПИН-кода на уровне пользователя или сайта, выполните следующие действия.

## Просмотр сведений о политике ПИН-кода в панели управления Lync Server

1.  Войдите на любой компьютер, подключенный к сети, где развернут Lync Server 2013, с использованием учетной записи, входящей в группу RTCUniversalServerAdmins (или имеющей равнозначные права пользователя) либо назначенной роли CsServerAdministrator или CsAdministrator.

2.  Откройте окно браузера и введите URL-адрес для администрирования, чтобы открыть панель управления Lync Server. Дополнительные сведения о различных методах, которые можно использовать для запуска панели управления Lync Server см. в разделе [Открытие средств администрирования Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  На панели навигации слева выберите **Безопасность** и нажмите **Политика ПИН-кода**.

4.  На странице **Политика ПИН-кода** щелкните политику, выберите **Изменить** и нажмите **Показать подробности**.

## Просмотр политик ПИН-кода с помощью командлетов Lync Server PowerShell

Для просмотра политик ПИН-кода можно также использовать Windows PowerShell и командлет Get-CsPinPolicy. Этот командлет можно выполнить из командная консоль Lync Server 2013 или из удаленного сеанса Windows PowerShell. Дополнительные сведения об использовании Windows PowerShell в удаленном режиме для подключения к Lync Server см. статью блога Lync Server Windows PowerShell "Краткое руководство: управление Microsoft Lync Server 2010 в удаленном режиме с помощью PowerShell" по адресу [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Просмотр политик ПИН-кода

  - Чтобы просмотреть сведения обо всех политиках ПИН-кода, введите в Командная консоль Lync Server следующую команду и нажмите ВВОД:
    
        Get-CsPinPolicy
    
    Возвращаются данные в следующем виде:
    
        Identity             : Global
        Description          :
        MinPasswordLength    : 5
        PINHistoryCount      : 0
        AllowCommonPatterns  : False
        PINLifetime          : 0
        MaximumLogonAttempts :

Дополнительные сведения см. в разделе справки по командлету [Get-CsPinPolicy](get-cspinpolicy.md).

## См. также

#### Задачи

[Изменение параметров конфигурации существующей веб-службы](lync-server-2013-modify-existing-web-service-configuration-settings.md)  
[Создание новой политики ПИН-кодов](lync-server-2013-create-a-new-pin-policy.md)
