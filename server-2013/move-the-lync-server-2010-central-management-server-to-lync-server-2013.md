﻿---
title: Перемещение центрального сервера управления Lync Server 2010 на Lync Server 2013
TOCTitle: Перемещение центрального сервера управления Lync Server 2010 на Lync Server 2013
ms:assetid: 30cc98f2-1916-4dbe-99d0-8df5368ed3ec
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ688013(v=OCS.15)
ms:contentKeyID: 49887931
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Перемещение центрального сервера управления Lync Server 2010 на Lync Server 2013

 

_**Дата изменения раздела:** 2013-11-25_

После миграции с Lync Server 2010 на Lync Server 2013 необходимо переместить центральный сервер управленияLync Server 2010 на сервер переднего планаLync Server 2013 или в пул, прежде чем можно будет удалить старый сервер Lync Server 2010.

Центральный сервер управления – это система с одним главным сервером и несколькими репликами, в которой чтение и запись копии базы данных выполняет сервер переднего плана, содержащий центральный сервер управления. На каждом компьютере в этой топологии, включая сервер переднего плана, содержащий центральный сервер управления, размещается доступная только для чтения копия данных из центрального хранилища управления в базе данных SQL Server (по умолчанию с именем RTCLOCAL), установленной на компьютере во время процесса установки и развертывания. Локальная база данных получает обновления реплики от агента репликации Lync Server, который выполняется в виде службы на всех компьютерах. Имя фактической базы данных на центральном сервере управления и локальной реплики – XDS, и она состоит из файлов xds.mdf и xds.ldf. Расположение базы данных master задается в точке управления службой (SCP) в доменных службах Доменные службы Active Directory. Все средства, использующие центральный сервер управления для управления и конфигурирования Lync Server, выполняют поиск расположения центрального хранилища управления с помощью SCP.

После успешного перемещения центрального сервера управления, необходимо удалить базы данных центрального сервера управления с исходного сервера переднего плана. Дополнительные сведения об удалении баз данных центрального сервера управления см. в статье [Удаление базы данных SQL Server для пула переднего плана](remove-the-sql-server-database-for-a-front-end-pool.md).

С помощью командлета Windows PowerShell**Move-CsManagementServer** в командной консоли Командная консоль Lync Server выполняется перемещение базы данных из SQL Server Lync Server 2010 в SQL Server Lync Server 2013, и значение SCP обновляется на расположение центрального сервера управления управленияLync Server 2013.

## Подготовка серверов переднего планаLync Server 2013 перед перемещением центрального сервера управления

Используйте процедуры, описанные в этом разделе, для подготовки переднего плана центрального сервера Lync Server 2013 перед перемещением центрального сервера управленияLync Server 2010.

## Порядок подготовки пула переднего плана Enterprise Edition

1.  В пуле переднего планаLync Server 2013 Enterprise Edition, в котором следует разместить центральный сервер управления: войдите в систему на компьютере, где установлена командная консоль Командная консоль Lync Server, в качестве члена группы **RTCUniversalServerAdmins**. Необходимо также иметь права и разрешения системного администратора базы данных SQL Server на базу данных, в которой требуется установить центральное хранилище управления.

2.  Откройте командную консоль Lync Server.

3.  Для создания нового центрального хранилища управления в базе данных SQL Server Lync Server 2013 в командной консоли Командная консоль Lync Server введите:
    
        Install-CsDatabase -CentralManagementDatabase -SQLServerFQDN <FQDN of your SQL Server> -SQLInstanceName <name of instance>

4.  Убедитесь, что состояние службы **Сервер переднего плана Lync Server** указано как **Запущена** .

## Порядок подготовки сервера переднего плана Standard Edition

1.  На сервере переднего планаLync Server 2013 Standard Edition, на котором следует разместить центральный сервер управления: войдите в систему на компьютере, где установлена командная консоль Командная консоль Lync Server, в качестве члена группы **RTCUniversalServerAdmins**.

2.  Откройте развертывания Lync Server.

3.  В мастере развертывания Lync Server выберите **Сначала подготовить сервер Standard Edition** .

4.  На странице **Выполнение команд** в качестве центрального сервера управления устанавливается SQL Server, экспресс-выпуск. Создаются необходимые правила брандмауэра. После завершения установки базы данных и предварительно устанавливаемого ПО нажмите кнопку **Готово** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>При первоначальной установке может пройти некоторое время, прежде чем на экране вывода результатов команд появятся какие-либо изменения. Так происходит, поскольку устанавливается SQL Server, экспресс-выпуск. Если необходимо отслеживать установку базы данных, используйте для этого диспетчер задач.</td>
    </tr>
    </tbody>
    </table>


5.  Для создания нового центрального хранилища управления на сервере переднего планаLync Server 2013 Standard Edition в командной консоли Командная консоль Lync Server введите:
    
        Install-CsDatabase -CentralManagementDatabase -SQLServerFQDN <FQDN of your Standard Edition Server> -SQLInstanceName <name of instance - RTC by default>

6.  Убедитесь, что состояние службы **интерфейсного сервера Lync** указано как **Запущена** .

## Порядок перемещения центрального сервера управленияLync Server 2010 на Lync Server 2013

1.  На сервере Lync Server 2013, который будет выполнять роль центрального сервера управления: войдите в систему на компьютере, где установлена командная консоль Командная консоль Lync Server, в качестве члена группы **RTCUniversalServerAdmins**. Необходимо также иметь права и разрешения администратора базы данных SQL Server.

2.  Откройте панель Командная консоль Lync Server.

3.  В командной консоли Командная консоль Lync Server введите:
    
        Enable-CsTopology
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412910.warning(OCS.15).gif" title="warning" alt="warning" />Предупреждение</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Если команда <code>Enable-CsTopology</code> не была выполнена успешно, прежде чем продолжить, устраните проблему, мешающую выполнению этой команды. В случае неудачного выполнения команды <strong>Enable-CsTopology</strong> перемещение не будет завершено и топология может остаться без центрального хранилища управления.</td>
    </tr>
    </tbody>
    </table>


4.  На сервере переднего плана или в пуле переднего планаLync Server 2013 в командной консоли Командная консоль Lync Server введите:
    
        Move-CsManagementServer

5.  В командой консоли Командная консоль Lync Server отображаются серверы, хранилища файлов, хранилища баз данных и точки подключения служб для текущего состояния и предложенного состояния. Внимательно просмотрите сведения об исходном и целевом состоянии и убедитесь, что они правильны. Введите **Y** , чтобы продолжить, или **N** , чтобы остановить перемещение.

6.  Проверьте все предупреждения и ошибки, сгенерированные командой **Move-CsManagementServer**, и устраните их.

7.  На сервере Lync Server 2013 откройте мастер развертывания Lync Server.

8.  В мастере развертывания Lync Server щелкните **Установить или обновить систему Lync Server** , щелкните **Шаг 2. Установить или удалить компоненты Lync Server** , нажмите кнопку **Далее** , просмотрите сводку, затем нажмите кнопку **Готово** .

9.  На сервере Lync Server 2010 откройте мастер развертывания Lync Server.

10. В мастере развертывания Lync Server щелкните **Установить или обновить систему Lync Server** , щелкните **Шаг 2. Установить или удалить компоненты Lync Server** , нажмите кнопку **Далее** , просмотрите сводку, затем нажмите кнопку **Готово** .

11. Перезагрузите сервер Lync Server 2013. Это требуется из-за изменения членства группы для доступа к базе данных управления.

12. Чтобы убедиться в том, что выполняется репликация нового центрального хранилища управления, в командной консоли Командная консоль Lync Server введите:
    
        Get-CsManagementStoreReplicationStatus
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Обновление всех текущих реплик может занять некоторое время.</td>
    </tr>
    </tbody>
    </table>


## Порядок удаления файлов центрального хранилища управленияLync Server 2010 после перемещения

1.  На сервере Lync Server 2010: войдите в систему на компьютере, где установлена командная консоль Командная консоль Lync Server, в качестве члена группы **RTCUniversalServerAdmins**. Необходимо также иметь права и разрешения администратора базы данных SQL Server.

2.  Откройте командную консоль Командная консоль Lync Server
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412910.warning(OCS.15).gif" title="warning" alt="warning" />Предупреждение</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Не удаляйте файлы старой базы данных, пока репликация не завершится и не станет стабильной. Если удалить файлы до завершения репликации, процесс репликации будет прерван и только что перемещенный центральный сервер управления останется в неопределенном состоянии. Используйте командлет <strong>Get-CsManagementStoreReplicationStatus</strong> для подтверждения состояния репликации.</td>
    </tr>
    </tbody>
    </table>


3.  Для удаления файлов базы данных центрального хранилища управления с центрального сервера управленияLync Server 2010 введите:
    
        Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn <FQDN of SQL Server> -SqlInstanceName <Name of source server>
    
    Например:
    
        Uninstall-CsDatabase -CentralManagementDatabase -SqlServerFqdn sql.contoso.net -SqlInstanceName rtc
    
    Здесь *\<FQDN of SQL Server\>* – это внутренний сервер Lync Server 2010 в развертывании Enterprise Edition или полное доменное имя сервера Standard Edition.
