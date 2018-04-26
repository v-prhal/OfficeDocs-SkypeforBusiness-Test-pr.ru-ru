﻿---
title: 'Lync Server 2013: определение требований DNS'
TOCTitle: Определение требований DNS
ms:assetid: 95777017-6282-44c0-a685-f246af0501b4
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg398758(v=OCS.15)
ms:contentKeyID: 49310553
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Определение требований DNS для Lync Server 2013

 

_**Дата изменения раздела:** 2016-12-08_

Для получения сведений о требованиях к службе доменных имен (DNS) используйте следующую блок-схему. Если применимы изменения для накопительных обновлений для сервера Lync Server 2013: февраль 2013 г., они указаны в соответствующих пунктах.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Microsoft Lync Server 2013 поддерживает IPv6-адреса. Для использования IPv6-адресов вам потребуется настроить DNS для поддержки протокола IP версии 6, а также настроить DNS-записи AAAA (также называемые &quot;четыре A&quot;). При наличии развертываний, в которых совместно используются IPv4- и IPv6-адреса, рекомендуется настроить как записи A для IP версии 4, так и записи AAAA для IP версии 6. Даже если развертывание полностью переведено на протокол IP версии 6, DNS-записи IP версии 4 могут потребоваться в случае, если внешние пользователи используют протокол IP версии 4.</td>
</tr>
</tbody>
</table>


**Определение требований DNS (блок-схема)**

![Блок-схема требований DNS](images/Gg398758.175782ac-363e-408a-912f-8991bf152970(OCS.15).jpg "Блок-схема требований DNS")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>По умолчанию имя компьютера, который не присоединен к домену, является именем узла, а не полным доменным именем. топологий использует полные доменные имена, а не имена узлов. Поэтому для компьютера, развертываемого в качестве пограничного сервера, не присоединенного к домену, вам потребуется указать DNS-суффикс. При назначении полных доменных имен серверам Lync Server, пограничным серверам и пулам <strong>используйте только стандартные символы</strong> (включая A–Z, a–z, 0–9 и дефисы). Не используйте символы Юникода или символы подчеркивания. Зачастую нестандартные символы в полном доменном имени не поддерживаются внешними DNS-серверами и общедоступными центрами сертификации (например, полное доменное имя должно быть назначено имени субъекта сертификата). Дополнительные сведения см. в разделе <a href="lync-server-2013-configure-dns-host-records.md">Настройка записей узлов DNS для Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


## Порядок обнаружения служб клиентами Lync

Процедуры Microsoft Lync 2010, Lync 2013 и Lync Mobile аналогичны процедурам поиска служб и осуществления доступа к ним клиентам в Lync Server 2013. Примечательным исключением является приложение Магазина Lync Windows, которое использует другой процесс обнаружения служб. В этом разделе приведены два сценария поиска служб клиентами; в первом сценарии задействован традиционный метод с использованием серии записей хоста A и SRV, а во втором сценарии используются только записи службы автоматического обнаружения. В накопительных пакетах обновления для настольных клиентов процесс обнаружения расположения DNS отличается от Lync Server 2010. Для всех клиентов процесс опроса DNS продолжается до тех пор, пока не будет возвращен успешный запрос или пока список возможных записей DNS не будет исчерпан и клиенту не будет возвращена окончательная ошибка.

Для всех клиентов, **кроме**Магазина Lync Windows, в ходе поиска DNS выполняется параллельный просмотр записей SRV. Клиент получает записи в следующем порядке:

1.  lyncdiscoverinternal. *\<домен\>*    запись A (хоста) для службы автоматического обнаружения на внутренних веб-службах

2.  lyncdiscover. *\<домен\>*    запись A (хоста) для службы автоматического обнаружения на внешних веб-службах

3.  \_sipinternaltls.\_tcp. *\<домен\>*    запись SRV (указателя служб) для внутренних подключений TLS

4.  \_sipinternal.\_tcp. *\<домен\>*    запись SRV (указателя служб) для внутренних подключений TCP (выполняется только в том случае, если протокол TCP разрешен)

5.  \_sip.\_tls. *\<домен\>*    запись SRV (указателя служб) для внешних подключений TLS

6.  sipinternal. *\<домен\>*    запись A (хоста) для переднего плана или Директор; разрешаемо только во внутренней сети

7.  sip. *\<домен\>*    запись A (хоста) для переднего плана или Директор во внутренней сети или доступа, когда клиент является внешним

8.  sipexternal. *\<домен\>*    запись A (хоста) для доступа, когда клиент является внешним

Магазина Lync Windows полностью изменяет этот процесс, так как используются две записи:

1.  lyncdiscoverinternal. *\<домен\>*    запись A (хоста) для службы автоматического обнаружения на внутренних веб-службах

2.  lyncdiscover. *\<домен\>*    запись A (хоста) для службы автоматического обнаружения на внешних веб-службах

Возможность восстановления других типов записей после отказа отсутствует.

Различие между методами, используемыми для новых клиентов, и методами, использованными для предыдущих клиентов, заключается в том, что служба автоматического обнаружения становится предпочтительным методам поиска всех служб.

После установления подключения служба автообнаружения возвращает все URL-адреса веб-служб для домашнего пула пользователя, включая URL-адреса служб Mobility Service (известных как Mcx в соответствии с виртуальным каталогом, созданным для службы в IIS), Microsoft Lync Web App и веб-планировщика. Однако внутренний и внешний URL-адрес службы Mobility Service связаны с полным доменным именем внешних веб-служб. Следовательно, независимо от того, является ли мобильное устройство внутренним или внешним по отношению к сети, устройство всегда будет подключаться к службе Mobility Service через обратный прокси-сервер.

Если установлены накопительные обновления для Lync Server 2013: февраль 2013 г., служба автообнаружения также возвращает ссылки на Internal/UCWA, External/UCWA и UCWA. Эти записи относятся к веб-компоненту веб-интерфейса API объединенных коммуникаций (UCWA). В настоящее время используется только запись UCWA и предоставляется ссылка на URL-адрес для веб-компонента. UCWA используется мобильными клиентами Lync 2013 вместо службы Mcx Mobility Service, используемой клиентами Lync 2010 Mobile.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>При создании записей SRV важно помнить, что они должны указывать на DNS-записи A и AAAA (при использовании IPv6-адресов) в том же домене, в котором была создана DNS-запись SRV. Например, если запись SRV относится к домену contoso.com, запись A и AAAA (если используется адресация IPv6), на которую она указывает, не может относиться к домену fabrikam.com.</td>
</tr>
</tbody>
</table>



> [!TIP]
> Конфигурация по умолчанию направляет весь трафик мобильного клиента через внешний сайт. Вы можете изменить параметры для возвращения только внутреннего URL-адреса, если это более предпочтительно в соответствии с вашими требованиями. В этой конфигурации пользователи смогут воспользоваться приложениями Lync Mobile на мобильных устройствах только при нахождении в сети организации. Для определения этой конфигурации необходимо использовать командлет <STRONG>Set-CsMcxConfiguration</STRONG>.



<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Несмотря на то что мобильные приложения также могут подключаться к остальным службам Lync Server 2013, например службе адресной книги, веб-запросы внутреннего мобильного приложения отправляются внешнему полному доменному имени только для службы Mobility Service. Для остальных запросов служб, например запросов адресной книги, эта конфигурация не требуется.</td>
</tr>
</tbody>
</table>


Мобильные устройства поддерживают обнаружение служб вручную. В этом случае каждому пользователю потребуется настроить параметры мобильного устройства с полным внутренним и внешним универсальными кодами ресурса (URI) службы автообнаружения, включая протокол и путь, следующим образом:

  - https:// *\<полное\_доменное\_имя\_внешнего\_пула\>* /Autodiscover/autodiscoverservice.svc/Root для внешнего доступа;

  - https:// *\<полное\_доменное\_имя\_внутреннего\_пула\>* /AutoDiscover/AutoDiscover.svc/Root для внутреннего доступа.

Вместо обнаружения вручную мы рекомендуем использовать автоматическое обнаружение. Однако обнаружение вручную позволяет устранять неполадки подключения мобильных устройств.

## Настройка разделенной DNS с помощью Lync Server

Разделенную службу доменных имен (DNS) иногда называют комбинированной DNS или расщеплением горизонта DNS. Под этим названием понимают конфигурацию DNS, в которой две зоны DNS имеют одно пространство имен, но при этом одна зона DNS обслуживает только внутренние запросы, а вторая зона DNS – только внешние запросы. Однако при этом большинство записей расположения службы (SRV) и записей A, содержащихся во внутренней DNS, будут отсутствовать во внешней DNS и наоборот. Если одна DNS-запись содержится во внутренней и внешней зоне DNS (например, www.contoso.com), возвращаемый IP-адрес будет зависеть от того, какая зона является источником запроса (внутренняя или внешняя).

<table>
<thead>
<tr class="header">
<th><img src="images/JJ618369.important(OCS.15).gif" title="important" alt="important" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>В настоящее время разделенная DNS не поддерживается для мобильной службы, а конкретнее для службы автообнаружения или записей DNS LyncDiscover и LyncDiscoverInternal. Запись LyncDiscover должна быть определена на внешнем DNS-сервере, а запись LyncDiscoverInternal – на внутреннем.</td>
</tr>
</tbody>
</table>


В этом разделе будет использоваться термин разделенная DNS.

Ниже приведены сводные данные о типах DNS-записей, требуемых для внутренней и внешней зоны, используемые при настройке разделенной DNS. Дополнительные сведения см. в разделе [Сценарии доступа внешних пользователей в Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md).

**Внутренняя DNS:**

  - Содержит доверенную зону DNS contoso.com.

  - Внутренняя зона contoso.com содержит:
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) и записи SRV для автоматической настройки внутреннего клиента Lync Server 2013 (необязательно).
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) или CNAME-записи для автоматического обнаружения веб-служб Lync Server 2013 (необязательно).
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) для имени интерфейсного пула, имени Директора или имени пула Директоров и всех внутренних серверов с установленным Lync Server 2013 в сети организации.
    
      - DNS-записи A и AAAA (при использовании адресации IPv6) для внутреннего пограничного интерфейса каждого Lync Server 2013 и пограничного сервера в сети периметра.
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) для внутреннего интерфейса каждого обратного прокси-сервера в сети периметра (необязательно для управления обратным прокси-сервером).
    
      - Для разрешения запросов к contoso.com все внутренние пограничные интерфейсы Lync Server 2013  сервер в сети периметра используют внутреннюю зону DNS.
    
      - Для разрешения запросов к contoso.com все серверы Lync Server 2013 и клиенты Lync 2013 в сети организации используют внутренние DNS-серверы либо используют файл HOSTS на каждом пограничном сервере и просматривают записи A и AAAA (при использовании IPv6-адресов) для сервера следующего прыжка, в частности Директора, виртуального IP-адреса Директора, виртуального IP-адреса интерфейсного пула или сервера Standard Edition.

**Внешняя DNS:**

  - Содержит доверенную зону DNS contoso.com.

  - Внешняя зона contoso.com содержит:
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) и записи SRV для автоматической настройки клиента Lync Server 2013 (необязательно).
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) или CNAME-записи для автоматического обнаружения веб-служб Lync Server 2013, предназначенных для функций мобильной связи.
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) и записи SRV для внешнего пограничного интерфейса каждого Lync Server 2013, пограничного сервера или виртуального IP-адреса аппаратного балансировщика нагрузки в сети периметра.
    
      - DNS-записи A и AAAA (при использовании IPv6-адресов) для внешнего интерфейса обратного прокси-сервера или виртуального IP-адреса пула обратных прокси-серверов в сети периметра.

## Автоматическая настройка без разделенной DNS

При использовании разделенной DNS пользователь Lync Server 2013, который выполняет вход из внутренней сети, может воспользоваться преимуществом автоматической настройки, если внутренняя зона DNS содержит запись SRV \_sipinternaltls.\_tcp для каждого используемого домена SIP. Однако если разделенная DNS не используется, то внутренняя автоматическая настройка клиентов Lync не будет работать до тех пор, пока не будет реализован один из обходных путей, описанных далее в этом разделе. Это связано с тем, что Lync Server 2013 требует, чтобы URI SIP пользователя совпадал с доменом интерфейсного пула, предназначенного для автоматической настройки. Это также имеет место в более ранних версиях Communicator.

Например, при использовании двух доменов SIP потребуются следующие записи службы DNS (SRV):

  - Если пользователь выполняет вход с учетной записью bob@contoso.com, то для автоматической настройки достаточно добавить следующую запись SRV, поскольку домен SIP пользователя (contoso.com) совпадает с доменом автоматической настройки интерфейсного пула:
    
     \_sipinternaltls.\_tcp.contoso.com. 86400 IN SRV 0 0 5061 pool01.contoso.com

  - Если пользователь выполняет вход с учетной записью alice@fabrikam.com, то для автоматической настройки второго домена SIP необходимо использовать следующую DNS-запись SRV.
    
     \_sipinternaltls.\_tcp.fabrikam.com. 86400 IN SRV 0 0 5061 pool01.fabrikam.com

Для сравнения: если пользователь выполняет вход с учетной записью tim@litwareinc.com, то для автоматической настройки нельзя использовать следующую DNS-запись SRV, поскольку домен SIP клиента (litwareinc.com) не совпадает с доменом, в котором находится пул (fabrikam.com):

 \_sipinternaltls.\_tcp.litwareinc.com. 86400 IN SRV 0 0 5061 pool01.fabrikam.com

Если для клиентов Lync требуется автоматическая настройка, то выберите один из следующих вариантов:

  - **Объекты групповой политики.**   Используйте объекты групповой политики (GPO) для добавления правильных серверных значений.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Этот вариант не включает автоматическую настройку, однако он автоматизирует процесс ручной настройки, поэтому при использовании этого варианта записи SRV, связанные с автоматической настройкой, не требуются.</td>
    </tr>
    </tbody>
    </table>


  - **Совпадающая внутренняя зона.**   Создайте зону во внутренней DNS, которая соответствует внешней зоне DNS (например, contoso.com), и создайте DNS-записи A и AAAA (при использовании IPv6-адресов), соответствующие пулу Lync Server 2013, используемому для автоматической настройки. Например, если пользователь расположен на сервере pool01.contoso.net, но выполняет вход в Lync с учетной записью bob@contoso.com, создайте внутреннюю зону DNS contoso.com, а затем внутри нее создайте DNS-запись A и AAAA (при использовании IPv6-адресов) для pool01.contoso.com.

  - **Точное определение внутренней зоны.**   Если по каким-либо причинам нельзя создать всю зону во внутренней DNS, вы можете создать точно заданные (выделенные) зоны, которые соответствуют записям SRV, требуемым для автоматической настройки, и затем заполнить их с помощью средства dnscmd.exe. Средство dnscmd.exe является обязательным, поскольку пользовательский интерфейс DNS не поддерживает создание точно заданных зон. Например, при наличии домена SIP contoso.com и интерфейсного пула pool01, который содержит два сервера переднего плана, вам потребуются следующие точно определенные зоны и записи A во внутренней DNS:
    
        dnscmd . /zoneadd _sipinternaltls._tcp.contoso.com. /dsprimary
        dnscmd . /recordadd _sipinternaltls._tcp.contoso.com. @ SRV 0 0 5061 pool01.contoso.com.
        dnscmd . /zoneadd pool01.contoso.com. /dsprimary
        dnscmd . /recordadd pool01.contoso.com. @ A 192.168.10.90
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
        dnscmd . /recordadd pool01.contoso.com. @ A 192.168.10.91 
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
    
    Если ваша среда содержит второй домен SIP (например, fabrikam.com), вам потребуются следующие точно определенные зоны и записи A во внутренней DNS:
    
        dnscmd . /zoneadd _sipinternaltls._tcp.fabrikam.com. /dsprimary
        dnscmd . /recordadd _sipinternaltls._tcp.fabrikam.com. @ SRV 0 0 5061 pool01.fabrikam.com.
        dnscmd . /zoneadd pool01.fabrikam.com. /dsprimary
        dnscmd . /recordadd pool01.fabrikam.com. @ A 192.168.10.90
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>
        dnscmd . /recordadd pool01.fabrikam.com. @ A 192.168.10.91
        dnscmd . /recordadd pool01.contoso.com. @ AAAA <IPv6 address>

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Полное доменное имя интерфейсного пула показано дважды, но с разными IP-адресами. Это связано с использованием балансировки нагрузки на DNS. Однако при использовании аппаратной балансировки нагрузки будет доступна только одна запись интерфейсного пула. Кроме того, значения полных доменных имен интерфейсного пула разные в примерах contoso.com и fabrikam.com, но IP-адреса остаются одинаковыми. Это связано с тем, что пользователи, выполняющие вход с любого домена SIP, используют для автоматической настройки один и тот же интерфейсный пул.</td>
</tr>
</tbody>
</table>


Дополнительные сведения см. в записи блога «Автоматическая конфигурация Communicator и разделенная DNS» в [http://go.microsoft.com/fwlink/p/?linkId=200707](http://go.microsoft.com/fwlink/p/?linkid=200707).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Содержимое всех блогов и их URL-адреса могут быть изменены без уведомления.</td>
</tr>
</tbody>
</table>


## Настройка DNS для аварийного восстановления

Чтобы настроить DNS для перенаправления веб-трафика Lync Server 2013 на сайты аварийного восстановления и отработки отказа, необходимо использовать поставщика DNS, который поддерживает GeoDNS. Можно настроить записи DNS для поддержки аварийного восстановления, чтобы компоненты, использующие веб-службы, продолжали работать даже при отказе одного пула переднего плана. Эта функция аварийного восстановления поддерживает простые URL-адреса автообнаружения (URL-адрес Lyncdiscover), собрания и телефонного подключения.

Определите и настройте дополнительные записи узлов DNS (A и AAAA, если используется IPv6) для внутреннего и внешнего разрешения веб-служб у поставщика GeoDNS. В приведенном ниже примере предполагается, что существуют географически разнесенные спаренные пулы и поставщик либо поддерживает GeoDNS с помощью циклического перебора DNS, либо настроен на использование пула Pool1 в качестве основного и пула Pool2 – для отработки отказа в случае потери связи или сбоя оборудования.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Запись GeoDNS (пример)</th>
<th>Записи пула (пример)</th>
<th>Записи CNAME (пример)</th>
<th>Параметры DNS (выберите один вариант)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Meet-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Meet.contoso.com для Pool1InternalWebFQDN.contoso.com</p>
<p>Псевдоним Meet.contoso.com для Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="even">
<td><p>Meet-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Meet.contoso.com для Pool1ExternalWebFQDN.contoso.com</p>
<p>Псевдоним Meet.contoso.com для Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="odd">
<td><p>Dialin-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Dialin.contoso.com для Pool1InternalWebFQDN.contoso.com</p>
<p>Псевдоним Dialin.contoso.com для Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="even">
<td><p>Dialin-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Dialin.contoso.com для Pool1ExternalWebFQDN.contoso.com</p>
<p>Псевдоним Dialin.contoso.com для Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="odd">
<td><p>Lyncdiscoverint-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Lyncdiscoverinternal.contoso.com для Pool1InternalWebFQDN.contoso.com</p>
<p>Псевдоним Lyncdiscoverinternal.contoso.com для Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="even">
<td><p>Lyncdiscover-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Lyncdiscover.contoso.com для Pool1ExternalWebFQDN.contoso.com</p>
<p>Псевдоним Lyncdiscover.contoso.com для Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="odd">
<td><p>Scheduler-int.geolb.contoso.com</p></td>
<td><p>Pool1InternalWebFQDN.contoso.com</p>
<p>Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Scheduler.contoso.com для Pool1InternalWebFQDN.contoso.com</p>
<p>Псевдоним Scheduler.contoso.com для Pool2InternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
<tr class="even">
<td><p>Scheduler-ext.geolb.contoso.com</p></td>
<td><p>Pool1ExternalWebFQDN.contoso.com</p>
<p>Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Псевдоним Scheduler.contoso.com для Pool1ExternalWebFQDN.contoso.com</p>
<p>Псевдоним Scheduler.contoso.com для Pool2ExternalWebFQDN.contoso.com</p></td>
<td><p>Циклический перебор между пулами</p>
<p>Используйте основной, в случае сбоя подключитесь к дополнительному</p></td>
</tr>
</tbody>
</table>


## Балансировка нагрузки на DNS

Балансировка нагрузки на DNS обычно реализуется на уровне приложений. Приложение (например, клиент Lync) пытается подключиться к серверу в пуле путем подключения к одному из IP-адресов, возвращаемых запросом DNS-записи A и AAAA (при использовании IPv6-адресов) для полного доменного имени пула.

Например, при наличии трех серверов переднего плана в пуле pool01.contoso.com выполняются следующие действия:

  - Клиенты Lync запрашивают pool01.contoso.com в DNS. Запрос возвращает 3 IP-адреса и кэширует их следующим образом (не обязательно в этом порядке):
    
    pool01.contoso.com      192.168.10.90
    
    pool01.contoso.com      192.168.10.91
    
    pool01.contoso.com      192.168.10.92

  - Клиент пытается установить подключение TCP к одному из IP-адресов. Если не удается установить подключение, клиент берет следующий IP-адрес из кэша.

  - Если подключение TCP успешно установлено, клиент согласует TLS для подключения к основному регистратору на pool01.contoso.com.

  - Если не удается установить подключение ни к одной кэшированной записи, пользователь получает уведомление о недоступности серверов Lync Server 2013.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Балансировка нагрузки на DNS отличается от циклического перебора DNS (DNS RR), который обычно относится к балансировке нагрузки с помощью DNS для обеспечения другого порядка IP-адресов, соответствующих серверам в пуле. Как правило, циклический перебор DNS обеспечивает только распределение нагрузки, но не отработку отказа. Например, если подключение к одному IP-адресу, возвращаемому запросом DNS-записи A и AAAA (при использовании IPv6-адресов), завершается с ошибкой, подключение разрывается. Следовательно, циклический перебор DNS является менее надежным, чем балансировка нагрузки на DNS. Вы можете использовать циклический перебор DNS вместе с балансировкой нагрузки на DNS.</td>
</tr>
</tbody>
</table>


Балансировка нагрузки на DNS используется в следующих целях:

  - Балансировка нагрузки SIP "сервер-сервер" до пограничных серверов.

  - Приложения балансировки нагрузки Unified Communications Application Services (UCAS), например автосекретарь, группа ответа и парковка. вызовов

  - Запрет новых подключений к приложениям UCAS (также называемое "сток").

  - Балансировка нагрузки всего трафика "клиент-сервер" между клиентами и пограничными серверами.

Балансировка нагрузки на DNS не может использоваться для выполнения следующих задач:

  - Веб-трафик "клиент-сервер" до Директора или серверов переднего плана.

Балансировка нагрузки на DNS и федеративный трафик:

Если на запрос записи SRV возвращается несколько DNS-записей, то пограничная служба доступа всегда выбирает DNS-запись SRV с наименьшим числовым приоритетом и наибольшим числовым весом. В документе Internet Engineering Task Force "A DNS RR для определения местоположения служб (DNS SRV)" <http://www.ietf.org/rfc/rfc2782.txt> указано, что, если определено несколько записей DNS SRV, сначала используется числовой приоритет, а затем вес. Например, запись A DNS SRV имеет числовой вес 20 и приоритет 40, а запись B DNS SRV имеет числовой вес 10 и приоритет 50. Будет выбрана запись A DNS SRV с приоритетом 40. Следующие правила применяются к выбору записи DNS SRV:

  - Сначала учитывается приоритет. Клиент ДОЛЖЕН пытаться связаться с целевым узлом, определяемым записью DNS SRV с самым низким числовым приоритетом, который может быть достигнут. Цели с одним и тем же приоритетом ДОЛЖНЫ достигаться в порядке, определяемым полем веса.

  - Поле веса определяет относительный вес для записей с одним и тем же приоритетом. Более крупный вес ДОЛЖЕН присваиваться при наличии пропорционально высокой вероятности выбора. Администраторы DNS ДОЛЖНЫ использовать вес 0 при отсутствии каких-либо серверных операций выбора, которые подлежат выполнению. При наличии записей, вес которых больше 0, крайне маловероятно, что будут выбраны записи, имеющие вес 0.

При получении нескольких DNS-записей SRV с равным приоритетом и весом пограничная служба доступа выберет запись SRV, которая была получена от DNS-сервера первой.
