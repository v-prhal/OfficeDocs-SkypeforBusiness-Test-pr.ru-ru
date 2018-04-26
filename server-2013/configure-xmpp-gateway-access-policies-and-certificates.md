﻿---
title: Настройка политик доступа и сертификатов шлюза XMPP
TOCTitle: Настройка политик доступа и сертификатов шлюза XMPP
ms:assetid: fac02f4e-d14d-4be3-b53c-74c82436fd93
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ721945(v=OCS.15)
ms:contentKeyID: 49888271
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Настройка политик доступа и сертификатов шлюза XMPP

 

_**Дата изменения раздела:** 2012-10-15_

Федерация XMPP определяет внешнее развертывание на основе протокола XMPP. Конфигурация XMPP позволяет пользователям Lync взаимодействовать с пользователями домена XMPP следующими способами:

  - обмен мгновенными сообщениями и сведениями о присутствии (только в двустороннем режиме);

  - создание федеративных контактов XMPP в клиенте Lync.

При настройке политик для поддержки протокола федеративных XMPP-партнеров эти политики применяются к пользователям федеративных доменов XMPP, но не к пользователям поставщиков услуг мгновенного обмена сообщениями SIP (например, Windows Live) или федеративных доменов SIP. Вы настраиваете федеративного XMPP-партнера для каждого федеративного домена XMPP, для которого хотите разрешить пользователям добавлять контакты и осуществлять взаимодействие. После задания политик вам необходимо настроить сертификаты шлюза XMPP.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Чтобы начать миграцию шлюза XMPP, вам необходимо развернуть шлюз XMPP системы Lync Server 2013 и настроить политики доступа, чтобы включить для пользователей поддержку шлюза XMPP системы Lync Server 2013. Перед выполнением этих действий следует переместить всех пользователей в развертывание системы Lync Server 2013. Дополнительные сведения см. в разделе <a href="configure-xmpp-gateway-on-lync-server-2013.md">Конфигурация шлюза XMPP на Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Настройка политики внешнего доступа для включения поддержки шлюза XMPP Lync Server 2013 у пользователей

1.  Откройте панель управления Lync Server.

2.  В левой панели навигации щелкните элемент **Федерация и внешний доступ** и затем элемент **Политика внешнего доступа** .

3.  Нажмите кнопку **Создать** и выберите **Политика пользователя** .

4.  Введите имя для политики внешнего доступа пользователя.

5.  Укажите описание для политики внешнего доступа пользователя.

6.  Выберите **Разрешить взаимодействие с федеративными пользователями** .

7.  Выберите **Разрешить связь с федеративными пользователями XMPP** .

8.  Нажмите кнопку **Commit** (Сохранить), чтобы сохранить изменения в политике на уровне сайта или пользователя.
