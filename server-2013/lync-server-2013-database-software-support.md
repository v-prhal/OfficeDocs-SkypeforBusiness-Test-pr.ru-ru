﻿---
title: 'Lync Server 2013: поддержка программного обеспечения баз данных'
TOCTitle: Поддержка программного обеспечения баз данных
ms:assetid: e05d0032-bbea-4e61-987d-d07b1c045fd5
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg398990(v=OCS.15)
ms:contentKeyID: 49311428
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Поддержка программного обеспечения баз данных в Lync Server 2013

 

_**Дата изменения раздела:** 2016-12-08_

Lync Server 2013 поддерживает следующие системы управления базами данных:

  - **Серверная база данных интерфейсного пула, база данных архивации, база данных мониторинга, база данных сохраняемого чата и база данных соответствия сохраняемого чата**
    
      - Программное обеспечение для баз данных Microsoft SQL Server 2008 R2 Enterprise (64-разрядная версия). Рекомендуется установить более новый пакет обновления.
    
      - Microsoft SQL Server 2008 R2 Standard (64-разрядная версия). Рекомендуется установить более новый пакет обновления.
    
      - Microsoft SQL Server 2012 Enterprise (64-разрядная версия). Рекомендуется установить более новый пакет обновления.
    
      - Microsoft SQL Server 2012 Standard (64-разрядная версия). Рекомендуется установить более новый пакет обновления.

  - **База данных сервера Standard Edition и базы данных переднего плана**
    
      - Microsoft SQL Server 2012 Express (64-разрядная версия). Рекомендуется установить более новый пакет обновления.
        
        Поддерживается исправление и обновление Microsoft SQL Server на переднего плана и выпуска Standard. Однако при выполнении исправления или обновления любого рода на переднего плана необходимо учитывать требования кворума. Подробнее см. разделы [Обновление серверов переднего плана в Lync Server 2013](lync-server-2013-upgrade-or-update-front-end-servers.md) и [Топология и компоненты для серверов переднего плана, обмена мгновенными сообщениями и сведениями о присутствии в Lync Server 2013](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Microsoft SQL Server 2012 Express (64-разрядная версия) автоматически устанавливается Lync Server 2013 на каждом сервере Standard Edition и каждом сервере переднего плана.</td>
    </tr>
    </tbody>
    </table>


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Система Lync Server 2013 не поддерживает 32-разрядную версию SQL Server. Вам следует использовать 64-разрядную версию.</p></li>
<li><p>SQL Server Web edition и SQL Server Workgroup Edition не поддерживаются. Вы не можете использовать их с системой Lync Server 2013.</p></li>
<li><p>Система Lync Server 2013 не поддерживает собственное зеркальное отображение базы данных.</p></li>
<li><p>Чтобы использовать роль сервера мониторинга, вам следует установить SQL Server Reporting Services.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Серверная база данных интерфейсного пула может быть установлена на отдельный компьютер SQL Server.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Если вы выравниваете базы данных Lync Server с другими базами данных, мы настоятельно рекомендуем оценить все факторы, которые могут повлиять га доступность и производительность, а также убедиться, что в случае сбоя одного узла другой узел сможет обрабатывать всю нагрузку. Для проверки возможностей отработки отказа мы рекомендуем провести тестирование для всех сценариев отработки отказа.</td>
</tr>
</tbody>
</table>


## Использование зеркального отображения и кластеризации SQL

Lync Server 2013 поддерживает использование как зеркального отображения SQL, так и кластеризации SQL для каждой базы данных Lync Server. Зеркальное отображение SQL настраивается с помощью средства топологий в Lync Server 2013. Для настройки отказоустойчивой кластеризации SQL необходимо использовать SQL Server.

Lync Server 2013 поддерживает зеркалирование SQL и топологии кластеров SQL для всех развертываний, включая развертывание с нуля и организации, в которых было выполнено обновление с предыдущих версий Lync Server.

Поддержка кластеризации SQL предназначена для активных и пассивных конфигураций. По соображениям производительности не следует предоставлять общий доступ к пассивному узлу для любого другого экземпляра SQL.

Включена поддержка описанных ниже функций.

  - Отказоустойчивая кластеризация двух узлов для указанных ниже продуктов.
    
      - Microsoft SQL Server 2012 Standard (64-разрядная версия). Рекомендуется установить более новый пакет обновления.
    
      - Microsoft SQL Server 2008 R2 Standard (64-разрядная версия). Рекомендуется установить более новый пакет обновления.

  - Отказоустойчивая кластеризации для узлов количеством до шестнадцати для указанных ниже продуктов.
    
      - Microsoft SQL Server 2012 Enterprise (64-разрядная версия). Рекомендуется установить более новый пакет обновления.
    
      - Программное обеспечение для баз данных Microsoft SQL Server 2008 R2 Enterprise (64-разрядная версия). Рекомендуется установить более новый пакет обновления.

Дополнительные сведения о зеркальном отображении SQL см. в статье [Высокая доступность внутреннего сервера в Lync Server 2013](lync-server-2013-back-end-server-high-availability.md). Подробные сведения о развертывании кластеров SQL см. в статье [Настройка кластеризации SQL Server в Lync Server 2013](lync-server-2013-configure-sql-server-clustering.md).

Дополнительные сведения и рекомендации по отказоустойчивой кластеризации в SQL Server 2012 см. в статье по адресу <http://technet.microsoft.com/ru-ru/library/hh231721.aspx>. Дополнительные сведения об отказоустойчивой кластеризации в SQL Server 2008 см. в статье по адресу <http://technet.microsoft.com/ru-ru/library/ms189134(v=sql.105).aspx>.
