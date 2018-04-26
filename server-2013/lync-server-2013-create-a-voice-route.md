﻿---
title: Создание голосового маршрута в Lync Server 2013
TOCTitle: Создание голосового маршрута в Lync Server 2013
ms:assetid: d189057d-cc9d-4622-9d10-f5385d703faf
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg398898(v=OCS.15)
ms:contentKeyID: 49311241
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Создание голосового маршрута в Lync Server 2013

 

_**Дата изменения раздела:** 2016-12-08_

Ниже приведена процедура создания нового маршрута голосовых вызовов с помощью панели управления Lync Server 2013. Процедура изменения существующего маршрута описана в статье [Изменение голосового маршрута в Lync Server 2013](lync-server-2013-modify-a-voice-route.md).

## Создание маршрута голосовых вызовов с помощью панели управления Lync Server

1.  Войдите на компьютер в качестве члена группы RTCUniversalServerAdmins или роли администратора **CsVoiceAdministrator**, **CsServerAdministrator** или **CsAdministrator**.

2.  Откройте окно браузера и введите URL-адрес для администрирования, чтобы открыть панель управления Lync Server. Дополнительные сведения о различных методах, которые можно использовать для запуска панели управления Lync Server см. в разделе [Открытие средств администрирования Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  В левой области навигации щелкните элемент **Маршрутизация голосовых вызовов**.

4.  Перейдите на вкладку **Route** (Маршрут).

5.  Нажмите кнопку **Создать**, чтобы вывести на экран диалоговое окно **Создание маршрута голосовых вызовов**.

6.  В поле **Name** (Имя) введите описательное имя маршрута голосовых вызовов.

7.  (Дополнительно). В поле **Description** (Описание) введите дополнительные сведения, описывающие маршрут голосовых вызовов.

8.  Чтобы указать шаблоны, которые будет включать этот маршрут, можно использовать средство **создания шаблона для сопоставления**, чтобы создать регулярное выражение или записать это выражение вручную.
    
      - Чтобы использовать средство **создания шаблона для сопоставления** для создания регулярного выражения, введите следующие значения. Можно указать два типа сопоставления шаблонов.
        
          - **Начальные цифры для разрешаемых номеров**. Введите значение префикса, который будет приниматься этим маршрутом (включая начальные символы и «+» при необходимости). Например, введите **+425**, а затем нажмите кнопку **Add** (Добавить). Повторите это действие для каждого значения префикса, который требуется включить в маршрут.
        
          - **Исключения**. Если необходимо указать одно или несколько исключений для значений префикса, выделите префикс и щелкните **Exceptions** (Исключения). Введите одно или несколько значений для сопоставляемых шаблонов, которые *не*должны приниматься этим маршрутом. Например, чтобы исключить из маршрута номера, начинающиеся на +425237, введите значение **+425237** в поле **Exceptions** (Исключения) и нажмите **ОК**.
    
      - Чтобы вручную определить соответствующие шаблоны, в средстве **создания шаблонов для сопоставления** нажмите кнопку **Edit** (Изменить), а затем введите регулярное выражение .NET Framework, чтобы указать соответствующий шаблон для целевых телефонных номеров, к которым применяется маршрут. Сведения о написании регулярных выражений см. в разделе «Регулярные выражения .NET Framework» статьи [http://go.microsoft.com/fwlink/?linkid=140927\&clcid=0x419](http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x419).

9.  Выберите **Блокировать АнтиАОН**, если требуется запретить отображение ИД телефона, с которого поступает исходящий вызов, для получателя звонка. Если выбрать этот вариант, необходимо указать **Альтернативный АнтиАОН**, который будет отображаться на экране телефона получателя.

10. Чтобы связать одну или несколько магистралей с маршрутом голосовых вызовов, нажмите кнопку **Добавить**, а затем выберите магистраль из списка.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Если развертывание включает любые серверы-посредники Microsoft Office Communications Server 2007 R2, они также будут доступны в списке.</td>
    </tr>
    </tbody>
    </table>


11. Чтобы связать одно или несколько использований PSTN с маршрутом голосовых звонков, нажмите кнопку **Select** (Выбрать) и выберите запись из списка записей использования PSTN, определенных для развертывания корпоративной голосовой связи.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Сведения о том, как просмотреть свойства каждой из доступных записей использования ТСОП, см. в статье <a href="lync-server-2013-view-pstn-usage-records.md">Просмотр записей использования ТСОП в Lync Server 2013</a>.<br />
    Сведения о создании и редактировании записей использования ТСОП см. в статьях <a href="lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md">Создание голосовой политики и настройка записей использования ТСОП в Lync Server 2013</a> и <a href="lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md">Изменение голосовой политики и настройка записей использования ТСОП в Lync Server 2013</a>.</td>
    </tr>
    </tbody>
    </table>


12. Чтобы оптимизировать производительность, рекомендуется упорядочить записи использования ТСОП. Чтобы изменить положение записи в списке, выделите имя записи и нажмите кнопку со стрелкой "вверх" или "вниз".
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>В отличие от политики голосовой связи, в которой порядок отображения записей использования PSTN является важным фактором, порядок перечисления записей использования PSTN в маршруте голосовых вызовов неважен. Тем не менее, рекомендуется упорядочить список, например по частоте использования: RedmondLocal, RedmondLongDist, RedmondInternational, RedmondBackup. (Lync Server проходит по списку сверху вниз.)</td>
    </tr>
    </tbody>
    </table>


13. (Дополнительно). Введите значение в поле **Введите преобразованное число для проверки** и нажмите кнопку **Перейти**. Результаты проверки отобразятся в области под полем.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Можно сохранить маршрут голосовых вызовов, который еще не прошел проверку, чтобы изменить его конфигурацию позднее. Дополнительные сведения см. в разделе <a href="lync-server-2013-test-voice-routing.md">Тестирование голосовой маршрутизации в Lync Server 2013</a>.</td>
    </tr>
    </tbody>
    </table>


14. Чтобы сохранить маршрут голосовых вызовов, нажмите кнопку **ОК**.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Каждый раз при создании маршрута голосовых вызовов необходимо запускать команду <strong>Commit All</strong> (Фиксировать все), чтобы опубликовать изменение в конфигурации. Дополнительные сведения см. в статье <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Публикация ожидающих изменений в конфигурации маршрутизации голосовой связи в Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## См. также

#### Задачи

[Изменение голосового маршрута в Lync Server 2013](lync-server-2013-modify-a-voice-route.md)  
[Просмотр записей использования ТСОП в Lync Server 2013](lync-server-2013-view-pstn-usage-records.md)  
[Создание голосовой политики и настройка записей использования ТСОП в Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[Изменение голосовой политики и настройка записей использования ТСОП в Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  
[Публикация ожидающих изменений в конфигурации маршрутизации голосовой связи в Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Другие ресурсы

[Тестирование голосовой маршрутизации в Lync Server 2013](lync-server-2013-test-voice-routing.md)
