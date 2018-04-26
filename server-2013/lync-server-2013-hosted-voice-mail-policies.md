﻿---
title: 'Lync Server 2013: политики размещенной голосовой почты'
TOCTitle: Политики размещенной голосовой почты
ms:assetid: d62a35ed-cbe2-4f06-86b4-e192c18435c1
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg398932(v=OCS.15)
ms:contentKeyID: 49311314
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Политики размещенной голосовой почты в Lync Server 2013

 

_**Дата изменения раздела:** 2012-10-01_

*Политика маршрутизации размещенной голосовой почты* предоставляет данные для приложения маршрутизации ExUM Lync Server 2013, относящиеся к маршрутизации вызовов для пользователей, почтовые ящики которых располагаются в размещаемой службе Exchange.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Политики маршрутизации размещенной голосовой почты требуются только для интеграции Lync Server 2013с размещаемой единой системой обмена сообщениями Exchange. Они не требуются для интеграции с локальной единой системой обмена сообщениями Exchange.</td>
</tr>
</tbody>
</table>


## Область действия политики маршрутизации размещенной голосовой почты

Область политики маршрутизации размещенной голосовой почты определяет иерархический уровень, на котором применяется политика. Можно настроить политики маршрутизации размещенной голосовой почты со следующими уровнями области.

  - *Глобальная* политика потенциально может влиять на всех пользователей в развертывании Lync Server 2013. Если для пользователя включен доступ к размещаемой единой системе обмена сообщениями Exchange, ему не назначена политика на пользователя и сайту пользователя не назначена политика сайта, применяется глобальная политика. Глобальная политика устанавливается в пределах сервера Lync Server 2013. Можно изменить ее в соответствии с конкретными потребностями; однако ее нельзя удалить или переименовать.

  - Политика *сайта* может влиять на всех пользователей, размещаемых в сайте, для которых определена политика. Если для пользователя настроен доступ к единой системой обмена сообщениями Exchange и ему не назначена политика на пользователя, применяется политика сайта.

  - Политика *на пользователя* может влиять только на отдельных пользователей или группы. Для применения политики на пользователя необходимо явно назначить политику отдельным пользователям, группам и контактным объектам.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Как правило, требуется только одна политика маршрутизации размещенной голосовой почты. Обычно используется глобальная политика, которую изменяют в соответствии с потребностями. При развертывании нескольких политик маршрутизации размещенной голосовой почты все такие политики имеют область действия, ограниченную пользователем.</td>
</tr>
</tbody>
</table>


## Атрибуты политики маршрутизации размещенной голосовой почты

Политика маршрутизации размещенной голосовой почты определяет два атрибута, которые приложение маршрутизации ExUM Lync Server 2013 вставляет в URI запроса сообщения INVITE, отправляемого в размещаемое внедрение единой системы обмена сообщениями Exchange.

  - **Назначение :** полное доменное имя размещаемой службы единой системы обмена сообщениями Exchange. Это значение используется локальным пограничным сервером Lync Server для выполнения маршрутизации.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Полное доменное имя Exchange Online – exap.um.outlook.com.</td>
    </tr>
    </tbody>
    </table>


  - **Организация :** полное доменное имя клиента размещаемой службы единой системы обмена сообщениями Exchange, в которой размещаются почтовые ящики пользователей Lync Server 2013. Политика голосовой почты может содержать несколько организаций. Этот атрибут должен представлять собой разделенный запятыми список клиентов Exchange Server, в которых размещаются почтовые ящики пользователей Lync Server 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Администратор клиента размещаемой службы единой системы обмена сообщениями Exchange должен предоставить необходимые значения для атрибутов &quot;Назначение&quot; и &quot;Организация&quot;. Чтобы настроить политику, необходимо запустить командлет New-CsHostedVoicemailPolicy или использовать командлет Set-CsHostedVoicemailPolicy для изменения существующей политики (например, глобальной политики).</td>
</tr>
</tbody>
</table>


Сведения об управлении политиками маршрутизации размещенной голосовой почты см. в описании следующих командлетов в документации Командная консоль Lync Server:

  - New-CsHostedVoicemailPolicy

  - Set-CsHostedVoicemailPolicy

  - Get-CsHostedVoicemailPolicy

## Назначение политики голосовой почты на пользователя

Если политика маршрутизации размещенной голосовой почты определяется для области на пользователя, ее требуется явно назначить. Чтобы назначить политику отдельным пользователям или группам, можно выполнить командлет Grant-CsHostedVoicemailPolicy.

Сведения о назначении или удалении политики на пользователя маршрутизации размещенной голосовой почты см. в описании следующих командлетов в документации Командная консоль Lync Server:

  - Grant-CsHostedVoicemailPolicy

  - Remove-CsHostedVoicemailPolicy
