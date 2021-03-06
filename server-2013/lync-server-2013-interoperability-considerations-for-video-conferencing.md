﻿---
title: Замечания по взаимодействию для видеоконференций
TOCTitle: Замечания по взаимодействию для видеоконференций
ms:assetid: 31ead3b5-ed95-42d4-96e2-7d9403d5c026
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ204790(v=OCS.15)
ms:contentKeyID: 49309363
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Замечания по взаимодействию для видеоконференций

 

_**Дата изменения раздела:** 2012-10-02_

В этом разделе описываются особенности работы пользователей на этапе сосуществования в процессе миграции, когда происходит взаимодействие между устаревшими клиентами и пулом Lync Server 2013 или клиентами Lync Server 2013 и устаревшим пулом.

## Пулы Lync Server 2013

Если устаревший клиент используется в пуле Lync Server 2013, в работе пользователей будут наблюдаться следующие особенности.

  - Для двусторонних звонков разрешение видео будет тем же, что и в устаревшем пуле.

  - В случае с многопользовательскими конференциями разрешение видео и доступные функции видеоконференций будут теми же, что и в устаревшем пуле. Развернутый вид и высокое разрешение недоступны.

## Устаревшие пулы

Если клиент Lync Server 2013 используется в устаревшем пуле, в работе пользователей будут наблюдаться следующие особенности.

  - В случае с двусторонними звонками в клиентах Lync Server 2013 могут использоваться следующие новые функции.
    
      - Видео стандарта H.264 доступно, если оба участника используют клиенты Lync Server 2013.
    
      - В клиенте Lync Server 2013 используется значение параметра TotalReceiveVideoBitRateKb по умолчанию, поскольку устаревший сервер не отправляет эти сведения при автоматической подготовке.

  - В случае с многопользовательскими конференциями разрешение видео и доступные функции видеоконференций будут теми же, что и при использовании устаревшего клиента в устаревшем пуле.

> [!NOTE]  
> Если клиент Lync Server 2013 размещается на устаревшем сервере, можно настроить пропускную способность для видеоконференций так, что все пользователи в пуле смогут получать видео только в низком разрешении, но отправлять в высоком. Например, можно присвоить параметру MaxVideoRateAllowed в конфигурации сервера-посредника значение CIF-250K, а параметру VideoBitRateKb в политике конференц-связи — значение 2000 кбит/с. В результате пользователи в пуле не смогут получать видео в высоком разрешении.<br />Поскольку параметр MaxVideoRateAllowed больше не используется для клиентов Lync Server 2013, с его помощью нельзя запретить клиентам Lync Server 2013 запрашивать видео в высоком разрешении. Вместо этого задайте для параметра VideoBitRateKb в политике конференц-связи для всех пользователей в пуле то же значение, что и для параметра MaxVideoRateAllowed (то есть CIF для скорости 250 кбит/с, VGA для скорости 600 кбит/с или HD для скорости 1500 кбит/с).
