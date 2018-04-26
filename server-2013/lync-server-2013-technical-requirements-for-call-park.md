﻿---
title: 'Lync Server 2013: технические требования к парковке вызовов'
TOCTitle: Технические требования к парковке вызовов
ms:assetid: 38bcf302-2b72-4492-9266-f6dc31b566e1
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ204818(v=OCS.15)
ms:contentKeyID: 49309465
ms.date: 07/21/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Технические требования к парковке вызовов в Lync Server 2013

 

_**Дата изменения раздела:** 2016-12-08_

В этом разделе описываются следующие технические требования для Приостановка вызовов:

  - Требования к оборудованию

  - Требования к программному обеспечению

  - Требования к портам

  - Требования к аудиофайлам

## Требования к оборудованию

приостановки вызовов предъявляет те же требования к оборудованию, что и переднего плана. Дополнительные сведения о требованиях к оборудованию см. в разделе [Аппаратные серверные платформы для Lync Server 2013](lync-server-2013-server-hardware-platforms.md) документации по обеспечению поддержки.

## Требования к программному обеспечению

приостановки вызовов предъявляет те же требования к операционной системе и обязательным программным компонентам, что и переднего плана. Дополнительные сведения о требованиях к программному обеспечению см. в разделе [Поддержка сервера и средств в операционной системе в Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) документации по обеспечению поддержки.

На всех серверах переднего плана и серверах Standard Edition, на которых развернуто приложение приостановки вызовов, необходима установка Windows Media Format Runtime для серверов под управлением Windows Server 2008 R2 или Microsoft Media Foundation для серверов под управлением Windows Server 2012 или Windows Server 2012 R2. Для Windows Server 2008 R2 Windows Media Format Runtime устанавливается как часть Windows Desktop Experience. Windows Media Format Runtime или Microsoft Media Foundation требуется для файлов Windows Media Audio (WMA-файлов), которые приложение Приостановка вызовов воспроизводит в качестве музыки при удержании вызова.

## Требования к портам

приостановки вызовов использует указанный ниже порт.

  - **порт 5075**   – используется для запросов прослушивания.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Этот порт является установкой по умолчанию, которую можно изменить с помощью командлета <strong>Set-CsApplicationServer</strong>. Сведения об этом командлете см. в документации по командной консоли Командная консоль Lync Server.</td>
</tr>
</tbody>
</table>


## Требования к аудиофайлам

Приложение приостановки вызовов поддерживает только файлы Windows Media Audio (WMA-файлы) для воспроизведения в качестве музыки при удержании. Чтобы настроить файлы для воспроизведения в качестве музыки при удержании, можно использовать Microsoft Expression Encoder 4. Чтобы загрузить Expression Encoder 4, см. раздел Expression Encoder 4 на странице [http://go.microsoft.com/fwlink/p/?linkId=202843](http://go.microsoft.com/fwlink/p/?linkid=202843). Это средство используется для преобразования файлов в формат WMA. Рекомендуемый формат для файлов музыки при приостановке вызовов Приостановка вызовов – Media Audio 9, 44 кГц, 16 бит, моно, CBR, 32 кбит/с.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Преобразованный файл воспроизводится на телефоне только на 16 кГц, даже если он был записан на 44 кГц.</td>
</tr>
</tbody>
</table>
