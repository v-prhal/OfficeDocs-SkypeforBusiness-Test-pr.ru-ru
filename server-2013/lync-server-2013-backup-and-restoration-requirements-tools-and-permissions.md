﻿---
title: 'Требования к резервному копированию и восстановлению: средства и разрешения'
TOCTitle: 'Требования к резервному копированию и восстановлению: средства и разрешения'
ms:assetid: 35ec2e33-f33e-4f84-9e64-6550fd78aa52
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Hh202171(v=OCS.15)
ms:contentKeyID: 52058186
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Требования к резервному копированию и восстановлению: средства и разрешения

 

_**Дата изменения раздела:** 2015-03-09_

В данном разделе описываются средства, которые вы можете использовать для резервного копирования и восстановления Lync Server 2013, указываются необходимые разрешения, а также возможность удаленного или локального выполнения команд. Основное внимание в данном разделе уделяется средствам резервного копирования и восстановления, входящим в состав Lync Server.

## Резервные копии

Чтобы выполнить резервное копирование Lync Server, используйте средства, указанные в следующей таблице. Все команды, необходимые для резервного копирования Lync Server, можно использовать в скриптах и выполнять удаленно.

### Средства для резервного копирования Lync Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Для резервного копирования данного объекта:</th>
<th>Используйте это средство или этот командлет:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Данные конфигурации топологии (Xds.mdf)</p></td>
<td><p>Export-CsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Данные службы информирования о местонахождении (E9-1-1) (Lis.mdf)</p></td>
<td><p>Export-CsLisConfiguration</p></td>
</tr>
<tr class="odd">
<td><p>Данные конфигурации группы ответа (RgsConfig.mdf)</p></td>
<td><p>Export-CsRgsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Сохраняемые пользовательские данные (база данных Rtcxds.mdf)</p>
<p>Идентификаторы конференций</p></td>
<td><p>Export-CsUserData</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>База данных архивации (LcsLog.mdf)</p></li>
<li><p>База данных мониторинга записей регистрации вызовов (LcsCDR.mdf)</p></li>
<li><p>База данных мониторинга качества взаимодействия (QoEMetrics.mdf)</p></li>
</ul></td>
<td><p>Средство работы с базами данных SQL Server, такое как SQL Server Management Studio</p></td>
</tr>
<tr class="even">
<td><p>База данных сохраняемого чата (Mgc.mdf)</p></td>
<td><p>Процедуры резервного копирования SQL Server или Export-CsPersistentChatData. Export-CsPersistentChatData экспортирует данные сохраняемого чата в виде файла.</p></td>
</tr>
<tr class="odd">
<td><p>Все хранилища файлов: хранилище файлов Lync Server, хранилище для архивации файлов</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Для файлов с именем <strong>Meeting.Active</strong> резервное копирование не требуется. Они используются и заблокированы во время проведения собрания.</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>Стандартное средство управления файловой системой, такое как Robocopy.</p></td>
</tr>
</tbody>
</table>


## Восстановление

Чтобы восстановить Lync Server, используйте средства, указанные в следующей таблице. Все команды, необходимые для восстановления Lync Server, можно использовать в скриптах. Некоторые из них можно запускать удаленно, однако остальные требуется запускать локально, как указано в следующей таблице.

### Средства для восстановления Lync Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Чтобы сделать это:</th>
<th>Используйте это средство или этот командлет:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Создание нового или чистого компьютера</p></td>
<td><ul>
<li><p>Программное обеспечение для установки операционной системы Windows</p></li>
<li><p>Программное обеспечение для установки SQL Server</p></li>
<li><p>Оснастка &quot;Сертификаты&quot; консоли управления (MMC) в случае восстановления сертификатов с экспортируемым закрытым ключом</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Восстановление данных хранилища файлов</p></td>
<td><p>Стандартное средство управления файловой системой, такое как Robocopy</p></td>
</tr>
<tr class="odd">
<td><p>Повторное создание пустых баз данных и установка разрешений для следующих компонентов:</p>
<ul>
<li><p>управления</p></li>
<li><p>Внутренний сервер</p></li>
<li><p>База данных мониторинга</p></li>
<li><p>База данных архивации</p></li>
</ul></td>
<td><p>Install-CsDatabase</p></td>
</tr>
<tr class="even">
<td><p>Восстановление указателя доменных служб Доменные службы Active Directory на центральное хранилище управления</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Если в какой-либо момент вы потеряете точку подключения службы, можете запустить этот командлет повторно.</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>Set-CsConfigurationStoreLocation</p></td>
</tr>
<tr class="odd">
<td><p>Импорт топологии, политик и параметров конфигурации в центральное хранилище управления (Xds.mdf)</p></td>
<td><p>Import-CsConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Публикация и активация топологии</p></td>
<td><p>топологий</p>
<p>-или-</p>
<p>Publish-CsTopology и Enable-CsTopology</p></td>
</tr>
<tr class="odd">
<td><p>Активация последней опубликованной топологии</p></td>
<td><p>Enable-CsTopology</p></td>
</tr>
<tr class="even">
<td><p>Переустановка компонентов Lync Server</p></td>
<td><p>Программа установки Lync Server</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Расположена в папке установки или на установочном носителе Lync Server в каталоге \setup\amd64\Setup.exe.</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="odd">
<td><p>Восстановление данных информирования о местонахождении (E9-1-1) (Lis.mdf)</p></td>
<td><p>Import-CsLisConfiguration</p></td>
</tr>
<tr class="even">
<td><p>Восстановление сохраняемых пользовательских данных (Rtcxds.mdf)</p></td>
<td><p>Import-CsUserData</p></td>
</tr>
<tr class="odd">
<td><p>Восстановление данных конфигурации группы ответа (RgsConfig.mdf)</p></td>
<td><p>Import-CsRgsConfiguration</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Если конфигурация восстанавливается в заново развернутом пуле, для которого в базе данных нет данных группы ответа, вам следует воспользоваться параметром –OverwriteOwner. Используйте его даже в том случае, если восстанавливаемые данные находятся в пуле с таким же полным доменным именем. В противном случае операция импорта будет выполнена с ошибкой, так как в Active Directory уже существуют контактные объекты для групп ответа.</td>
</tr>
</tbody>
</table>

</div></td>
</tr>
<tr class="even">
<td><p>Восстановление следующих баз данных:</p>
<ul>
<li><p>База данных архивации (LcsLog.mdf)</p></li>
<li><p>Базы данных мониторинга: база данных записей регистрации вызовов (LcsCDR.mdf) и база данных качества взаимодействия (QoEMetrics.mdf)</p></li>
</ul></td>
<td><p>Средства управления базами данных SQL Server</p></td>
</tr>
<tr class="odd">
<td><p>База данных сохраняемого чата (Mgs.mdf)</p></td>
<td><p>Процедуры восстановления SQL Server или Import-CsPersistentChatData. Вы можете использовать Import-CsPersistentChatData с файлом, созданным Export-CsPersistentChatData, в результате чего данные импортируются в базу данных сохраняемого чата.</p></td>
</tr>
</tbody>
</table>


## Требуемые разрешения

Для выполнения всех описанных в разделе команд пользователи должны быть членами группы **RTCUniversalServerAdmins**. Большинство команд резервного копирования и восстановления не поддерживает управление доступом на основе ролей (RBAC). В качестве исключений можно назвать два командлета сохраняемого чата — Export-CsPersistentChatData и Import-CsPersistentChatData, которые должны выполняться пользователем, являющимся членом группы CsPersistentChatAdministrator. Чтобы запустить мастер развертывания Lync Server пользователь также должен быть членом группы локальных администраторов.

