﻿---
title: 'Lync Server 2013: планирование емкости для группы ответа'
TOCTitle: Планирование емкости для группы ответа
ms:assetid: a2459a69-1f45-4f2f-bca5-d4f442708e44
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg412754(v=OCS.15)
ms:contentKeyID: 49310726
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Планирование емкости для группы ответа в Lync Server 2013

 

_**Дата изменения раздела:** 2015-03-09_

В следующей таблице описывается пользовательская модель ответа, которую можно взять за основу при определении требований к планированию мощности.

> [!NOTE]  
> Значения приведены для звуковых файлов группы ответа со следующими характеристиками: 16-разрядный файл с расширением WAV и частотой 16 кГц в монофонической записи. Если вы используете другие форматы файлов, например Windows Media Audio (WMA), характеристики могут отличаться.

> [!IMPORTANT]  
> При планировании мощности аварийного восстановления для парных пулов необходимо учитывать, что каждый пул, входящий в состав парного пула, должен обрабатывать рабочие нагрузки всех групп ответа в обоих пулах.

### Пользовательская модель группы ответа

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Показатель</th>
<th>Для каждого пула Enterprise Edition (содержит 8 серверов переднего плана)</th>
<th>Для каждого сервера Standard Edition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Входящих звонков в секунду</p></td>
<td><p>16</p></td>
<td><p>2</p></td>
</tr>
<tr class="even">
<td><p>Число звонков, одновременно подключенных к интерактивному автоответчику или находящихся на удержании</p></td>
<td><p>480</p></td>
<td><p>60</p></td>
</tr>
<tr class="odd">
<td><p>Число одновременных анонимных сеансов (без учета сеансов обмена мгновенными сообщениями)</p></td>
<td><p>224</p></td>
<td><p>28</p></td>
</tr>
<tr class="even">
<td><p>Число одновременных анонимных сеансов (с учетом сеансов обмена мгновенными сообщениями)</p></td>
<td><p>64</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>Число активных агентов (официальные и неофициальные)</p></td>
<td><p>1200</p></td>
<td><p>1200</p></td>
</tr>
<tr class="even">
<td><p>Число сервисных групп</p></td>
<td><p>400</p></td>
<td><p>400</p></td>
</tr>
<tr class="odd">
<td><p>Число групп интерактивного автоответчика (распознавание речи)</p></td>
<td><p>200</p></td>
<td><p>200</p></td>
</tr>
</tbody>
</table>

