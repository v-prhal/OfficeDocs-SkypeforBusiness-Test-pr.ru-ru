﻿---
title: Распределение нагрузки для конференц-связи
TOCTitle: Распределение нагрузки для конференц-связи
ms:assetid: 5901a076-1b6f-4720-8837-95fc7f3c37f3
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ204922(v=OCS.15)
ms:contentKeyID: 49309852
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Распределение нагрузки для конференц-связи

 

_**Дата изменения раздела:** 2012-10-22_

В отличие от некоторых специальных решений конференц-связи архитектура Lync Server построена на модели совместно используемого оборудования. Это означает, что одно и то же оборудование совместно используется многими программными компонентами, каждый из которых поддерживает в режиме реального времени различные виды связи, которые, в свою очередь, подвергают серверы определенным нагрузкам. Например, сервер переднего плана может работать с компонентами маршрутизации SIP, веб-приложениями (такими как поиск по адресной книге), приложениями веб-конференций, аудио- и видеоконференций, корпоративной голосовой связи (например, помощника по конференц-связи и "Группа ответа"), а также с сервером-посредником. Набор баз данных на интерфейсном сервере также предоставляет хранилище и возможности обработки пользователей, контактов, состояния присутствия, конференций и данных маршрутизации голосовой связи. Благодаря этому совместному использованию оборудования компоненты, службы и процессы пытаются получить ресурсы ЦП и памяти, поэтому загрузки, не связанные с конференциями, имеют непосредственное влияние на масштабирование сервера.

По сравнению с другими решениями конференц-связи на основе портов архитектура конференций Lync Server является моделью без резервирования. Если пользователь планирует собрание, Lync Server создает запись в базе данных конференц-связи, куда сохраняются данные конференции, но не резервирует заблаговременно какие-либо аппаратные ресурсы для запланированного собрания. Вместо этого Lync Server имеет встроенную логику балансировки нагрузки для динамического выделения ресурсов для конференц-связи на серверах переднего плана, чтобы нагрузки распределялись равномерно по всем серверам переднего плана в пуле. Это позволяет эффективно выделять и использовать ресурсы оборудования, однако затрудняет поддержку очень больших собраний (особенно без соответствующего планирования). Например, если пул Lync Server 2013 используется практически на полную мощность, каждый сервер переднего плана может поддерживать приблизительно 125 средних по размеру собраний. Добавление еще одного маленького собрания останется незамеченным, однако добавление собрания с участием 1000 пользователей станет настоящей проблемой, так как серверы переднего плана, скорее всего, не смогут поддерживать настолько крупное собрание одновременно с другими 125 собраниями.

