﻿---
title: Использование подробного журнала для искусственных транзакций
TOCTitle: Использование подробного журнала для искусственных транзакций
ms:assetid: 32714a71-9f42-4d5b-a508-e176d8f08bbf
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ204798(v=OCS.15)
ms:contentKeyID: 49309371
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Использование подробного журнала для искусственных транзакций

 

_**Дата изменения раздела:** 2012-10-22_

Искусственные транзакции (представленные в Microsoft Lync Server 2010) предоставляют администраторам возможность подтверждения того, что пользователи могут успешно выполнять типичные задачи, такие как вход в систему, обмен мгновенными сообщениями или выполнение вызовов на телефон, расположенный в коммутируемой телефонной сети. Эти тесты (который упакованы как набор командлетов Windows PowerShellLync Server) может вручную выполнять администратор; они могут также автоматически выполняться таким приложением, как System Center Operations Manager.

В Lync Server 2010 искусственные транзакции являются чрезвычайно полезными для администраторов, так как они помогают идентифицировать проблемы с системой; например, командлет **Test-CsRegistration** может предупреждать администраторов о том, что некоторые пользователи сталкиваются с трудностями при регистрации с Lync Server. Однако искусственные транзакции оказались не настолько эффективными, чтобы помогать администраторам определять, почему эти пользователи сталкиваются с трудностями при регистрации в Lync Server. Это объяснялось тем фактом, что искусственные транзакции не предоставляли подробных сведений, которые могли бы помочь администраторам диагностировать проблемы с Lync Server. В лучшем случае подробные выходные данных искусственной транзакции содержали пошаговые сведения, на основе которых администратор мог сделать обоснованное предположение относительно того, где, вероятнее всего, возникла проблема.

В Microsoft Lync Server 2013 искусственные транзакции были переконструированы таким образом, чтобы обеспечить расширенную регистрацию данных. «Расширенная регистрация» означает, что для каждой операции, выполняемого искусственной транзакцией, регистрируется следующая информация:

  - Время начала операции

  - Время завершения операции

  - Действие, которое было выполнено (например, создание конференции, присоединение к ней или выход из нее, вход в Lync Server, отправка мгновенного сообщения и т. д.)

  - Информационные, подробные сообщения, предупреждения или сообщения об ошибках, которые были созданы при выполнении операции

  - Сообщения о регистрации SIP

  - Записи об исключениях или диагностические коды, созданные при выполнении операции

  - Итоговый результат выполнения операции

Эта информация создается автоматически при каждом запуске искусственной транзакции. Однако автоматическое отображение или сохранение сведений в файл журнала не выполняется. Вместо этого администраторы, запускающие искусственную транзакцию вручную, могут использовать параметр OutLoggerVariable для указания переменной Windows PowerShell, в которой будет сохраняться информация. Затем администраторы смогут применять несколько методов, позволяющих сохранять и/или просматривать полный журнал в формате XML или HTML.

Например, администраторы Lync Server 2010 могут выполнять командлет **Test-CsRegistration**, используя команду, аналогичную следующей:

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com

Администраторы могут включить параметр OutLoggerVariable с последующим именем переменной по своему выбору:

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -OutLoggerVariable RegistrationTest

> [!NOTE]  
> Имени переменной не должен предшествовать символ $. Например, используйте имя переменной RegistrationTest, а не $RegistrationTest.

Предыдущая команда выводит содержимое, аналогичное следующему:

    Target Fqdn   : atl-cs-001.litwareinc.com
    Result        : Failure
    Latency       : 00:00:00
    Error Message : This machine does not have any assigned certificates.
    Diagnosis     :

Однако для данного сбоя доступна гораздо более подробная информация, а не только сообщение об ошибке, представленное выше. Для получения доступа к этой информации в формате HTML используйте команду, аналогичную этой, чтобы сохранить данные, хранящиеся в переменной RegistrationTest, в файл HTML:

    $RegistrationTest.ToHTML() | Out-File C:\Logs\Registration.html

Можно также использовать метод ToXML() для сохранения данных в файл XML:

    $RegistrationTest.ToXML() | Out-File C:\Logs\Registration.xml

Эти файлы затем можно просматривать с помощью Internet Explorer, Visual Studio или любого другого приложения, поддерживающего открытие файлов HTML/XML.

Искусственные транзакции, запускаемые из System Center Operations Manager, будут автоматически генерировать эти файлы журнала в случае сбоев. Однако эти журналы не будут созданы, если сбой выполнения произойдет до того, как Windows PowerShell загрузит и запустит искусственную транзакцию.

> [!IMPORTANT]  
> По умолчанию Lync Server 2013 сохраняет файлы журнала в папке. Для обеспечения простого и быстрого доступа к этим журналам необходимо открыть общий доступ к этой папке (например, \\atl-watcher-001.litwareinc.com\WatcherNode.
