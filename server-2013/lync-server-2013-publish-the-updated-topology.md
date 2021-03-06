﻿---
title: 'Lync Server 2013: публикация обновленной топологии'
TOCTitle: Публикация обновленной топологии
ms:assetid: 59455dd1-6a9e-433f-a714-d3636c068100
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ204910(v=OCS.15)
ms:contentKeyID: 49309854
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Публикация обновленной топологии в Lync Server 2013

 

_**Дата изменения раздела:** 2012-10-01_

После обновления топологии в топологий необходимо опубликовать топологию в управления, прежде чем вы сможете настраивать и использовать сохраняемого сеанса беседы. Доступные только для чтения копии данных реплицируются на все серверы в топологии, чтобы обеспечивать синхронизацию всех серверов для внесения изменений топологии и других изменений конфигурации.

## Публикация обновленной топологии

Перед публикацией топологии установите базы данных для сервера сохраняемого сеанса беседы. Используйте построитель топологий для установки баз данных путем выбора **Действие** и **Установить базу данных** .

1.  На компьютере, на котором выполняется Lync Server 2013 или на котором установлены средства администрирования Lync Server выполните вход в систему, используя учетную запись, которая является членом и группы **Domain Admins**, и группы **RTCUniversalServerAdmins** и обладает полными правами на управление (то есть правами на чтение, запись и изменение) хранилищем файлов, чтобы использовать ее для хранилища файлов сохраняемого сеанса беседы (чтобы предоставить топологий возможности настройки необходимых списков DACL). Можно также использовать учетную запись с аналогичными правами пользователя.

2.  Запустите планировщик топологий. Выберите пункт **Загрузить топологию из существующего развертывания** или **Открыть топологию из локального файла** , если она сохранена локально.

3.  В дереве консоли щелкните правой кнопкой мыши **Lync Server 2013**, а затем щелкните **Опубликовать топологию** .

4.  На странице **Publish the topology** (Публикация топологии) нажмите кнопку **Next** (Далее).

5.  На странице **Завершение мастера публикации** убедитесь, что топология была успешно опубликована, а затем щелкните **Готово** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>После публикации топологии необходимо настроить поддержку сохраняемого сеанса беседы; архивация любого содержимого возможна только после выполнения этого действия.</td>
    </tr>
    </tbody>
    </table>

