﻿---
title: 'Lync Server 2013: еженедельные задачи'
TOCTitle: Еженедельные задачи
ms:assetid: d564839b-b49d-4c5d-b67e-dc5abb0f6980
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dn722432(v=OCS.15)
ms:contentKeyID: 62282849
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Еженедельные задачи в Lync Server 2013

 

_**Дата изменения раздела:** 2016-12-08_

Еженедельные задачи обычно относятся к сбору и анализу журналов и отчетов.

## Архивация журналов событий

Если журналы событий не настроены на перезапись событий должным образом, их необходимо регулярно архивировать и удалять. Данное действие особенно важно для журналов безопасности, которые могут потребоваться при исследовании попыток нарушения системы безопасности.

Вашей организации необходимо будет определить политики и процедуры для архивации журнала.

## Создание отчетов

Создайте отчеты о состоянии для помощи в планировании емкости, обзоров соглашений об уровне обслуживания и анализа производительности. Используйте ежедневные данные из журнала событий и системного монитора для создания отчетов об использовании диска, памяти и ЦП. Используйте System Center Operations Manager для формирования отчетов о времени работы и доступности.

Вашей организации необходимо определить политики и процедуры для отчетов о состояниях.

## Отчеты об инцидентах

Выполняйте еженедельный аудит отчетов об инцидентах вашей организации, которые относятся к Lync Server. Данный аудит должен включать в себя следующие пункты:

  - Основные сформированные, разрешенные и отложенные инциденты.

  - Решения для нерешенных инцидентов.

  - Обновление отчетов для включения в них новых уведомлений о неисправностях.

  - Обновление репозитория документов для руководств по устранению неполадок и публикация анализа о простоях.

Так как система отслеживания инцидентов вашей организации является независимым от Lync Server выбором, определенные инструкции или указатели недоступны. Обратитесь к документации для выбранной организацией системы.

## Проверка журналов IIS и производительности

Выполняйте еженедельный обзор журналов Службы IIS и производительности. Дополнительные сведения о способе мониторинга журналов IIS и производительности см. в статье [Windows Server 2003 Internet Information Services (IIS): Обзор ведения журнала событий](http://go.microsoft.com/fwlink/?linkid=36077). Обзор должен содержать следующие пункты:

  - Счетчики кэша веб-службы для мониторинга кэш-памяти службы WWW.

  - Счетчики страниц Active Server Pages (ASP) для мониторинга приложений, которые запущены как страницы ASP.

Дополнительные сведения о способе мониторинга журналов IIS и производительности см. в статье [Windows Server 2003 Internet Information Services (IIS): Обзор ведения журнала событий](http://go.microsoft.com/fwlink/?linkid=36077).

## Создание отчетов базы данных

**Способ создания отчетов для базы данных SQL**

1.  Откройте Lync Server 2013.

2.  В дереве консоли разверните узел леса, затем **корпоративные пулы** и выберите пул, для которого необходимо создать отчет базы данных.

3.  В области сведений нажмите вкладку **База данных**.

4.  На вкладке **База данных** выполните следующие действия:
    
    1.  Для просмотра имени базы данных разверните пункт **Общие параметры** и найдите имя базы данных.
    
    2.  Для извлечения текущей сводной статистики пользователя для пула разверните пункт **Сводные отчеты пользователя**, нажмите **Перейти** и просмотрите результаты.
    
    3.  Для просмотра текущих данных на уровне пользователя для одного пользователя в пуле разверните пункт **Отчеты на уровне пользователя**, введите пользовательский код URI для SIP, нажмите **Перейти** и просмотрите результаты.

Для просмотра текущей сводной статистики конференции для пула разверните пункт **Сводные отчеты по конференции**, нажмите **Перейти** и просмотрите результаты.

## Проверка безопасности и обновлений Lync Server

Определите любые новые пакеты обновления, исправления или обновления. При необходимости проверьте их в лаборатории тестирования и используйте процедуры изменения контроля для упорядочения развертывания на производственных серверах. Также теперь доступны обновления компонента Lync Server как части обновления Windows. Все обновления компонента Lync Server должны быть обновлены в одно время на всех серверах под управлением Lync Server, для которых данные обновления применимы.

## Запуск анализатора соответствия рекомендациям Lync Server 2013

Инструмент анализатора соответствия рекомендациям Lync Server 2013является диагностическим инструментом, который собирает информацию о конфигурации и определяет, установлена ли конфигурация в соответствии с рекомендациями Microsoft. Документацию для данного инструмента можно найти в статье [Анализатор соответствия рекомендациям Lync Server 2013](lync-server-2013-lync-server-best-practices-analyzer.md) и [Run Best Practices Analyzer](https://technet.microsoft.com/ru-ru/library/gg398652\(v=ocs.15\)).

Инструмент сравнивает данные конфигурации развертывания с набором предустановленных правил для Lync Server и сообщает о потенциальных неполадках. Для каждой обнаруженной неполадки предоставляется текущая конфигурация в среде Lync Server и рекомендованная конфигурация.

С помощью правильного сетевого доступа инструмент может обследовать AD DS и серверы под управлением Lync Server 2013 в рамках выполнения следующих действий:

  - профилактическое выполнение проверок работоспособности с проверкой установки конфигурации в соответствии с рекомендациями;

  - создание списка проблем, таких как неоптимальные параметры конфигурации, неподдерживаемые параметры или нерекомендуемые параметры;

  - оценка общей работоспособности системы;

  - помощь в устранении определенных неполадок;

  - запрос на загрузку обновлений (если доступны);

  - предоставление интерактивной и локальной документации о сообщенных неполадках, включая советы по их устранению;

  - создание информации о конфигурации, которую можно собрать для последующего обзора.

Убедитесь, что RTCBPA.msi установлен на всех серверах Lync Server 2013 и создайте еженедельный отчет о проверке работоспособности. Обратите внимание на результаты и при необходимости внесите исправления.

## Обзор значений производительности соглашения об уровне обслуживания

Проверьте ключевые данные производительности для предыдущей недели. Просмотрите производительность относительно требований соглашения об уровне обслуживания. Определите тенденции и элементы, которые не соответствуют целям.

## Просмотр отчетов пакета управления System Center Operations Manager и качества использования

Получите и просмотрите отчеты пакета управления Lync Server 2013 и качества использования.

## Создание и просмотр отчетов базы данных для корпоративных пулов

**Способ создания отчетов о пулах**

1.  Откройте Lync Server 2013.

2.  В дереве консоли разверните узел леса, затем **корпоративные пулы** и выберите пул, для которого необходимо создать отчет базы данных.

3.  В области сведений нажмите вкладку **База данных**.

4.  На вкладке **База данных** выполните следующие действия:
    
    1.  Для просмотра имени базы данных разверните пункт **Общие параметры** и найдите имя базы данных.
    
    2.  Для извлечения текущей сводной статистики пользователя для пула разверните пункт **Сводные отчеты пользователя**, нажмите **Перейти** и просмотрите результаты.
    
    3.  Для просмотра текущих данных на уровне пользователя для одного пользователя в пуле разверните пункт **Отчеты на уровне пользователя**, введите пользовательский код URI для SIP, нажмите **Перейти** и просмотрите результаты.

Для просмотра текущей сводной статистики конференции для пула разверните пункт **Сводные отчеты по конференции**, нажмите **Перейти** и просмотрите результаты.

Для каждого корпоративного пула администраторы могут использовать вкладку **База данных** для просмотра имени базы данных, а также извлечения и просмотра отчетов из базы данных.

### Отчеты базы данных и описания

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Раздел</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Сводные отчеты пользователя</p></td>
<td><p>Dbanalyze /v /report:diag [/sqlserver:value]</p>
<p>В данном разделе представлена объединенная информация о пользователях в пулах, такая как количество допустимых пользователей, среднее количество контактов для пользователя и количество пользователей для определенных возможностей.</p>
<p>При использовании данных отчетов следующая информация может быть полезной.</p>
<ul>
<li><p>Допустимый пользователь — это пользователь, которому разрешено использование Lync Server 2013 с помощью оснастки &quot;Пользователи и компьютеры&quot; Active Directory.</p></li>
<li><p>Активный пользователь — это пользователь, который выполнил вход или зарегистрировался.</p></li>
<li><p>Сводные отчеты также предлагают набор статистической информации о контактах. Данная статистика предназначена только для обычных пользователей, которые выполнили вход не менее одного раза, а также имеют не менее одного контакта. Следовательно, как правило, вы не видите минимального количества контактов равное нулю. Благодаря данному поведению, если у пользователя отсутствуют контакты (но он считается активным из-за своей регистрации), можно увидеть значение &lt;пусто&gt; для некоторых полей статистики.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Отчеты на уровне пользователя</p></td>
<td><p>Dbanalyze /v /report:disk [/sqlserver:value]</p>
<p>В отличие от сводных отчетов, которые вычисляются на основе общего количества пользователей, эти отчеты характерны для определенного пользователя.</p></td>
</tr>
<tr class="odd">
<td><p>Сводные отчеты по конференции</p></td>
<td><p>Dbanalyze /v /report:conf [/sqlserver:value]</p>
<p>В данном разделе представлена объединенная информация о сводной статистике конференции для пула, такая как количество активных конференций и общее число участников.</p></td>
</tr>
<tr class="even">
<td><p>Сводные отчеты пользователя</p></td>
<td><p>Dbanalyze /v /report:diag [/sqlserver:value]</p>
<p>В данном разделе представлена объединенная информация о пользователях в пулах, такая как количество допустимых пользователей, среднее количество контактов для пользователя и количество пользователей для определенных возможностей.</p>
<p>При использовании данных отчетов следующая информация может быть полезной.</p>
<ul>
<li><p>Допустимый пользователь — это пользователь, которому разрешено использование Lync Server 2013 с помощью оснастки &quot;Пользователи и компьютеры&quot; Active Directory.</p></li>
<li><p>Активный пользователь — это пользователь, который выполнил вход или зарегистрировался.</p></li>
<li><p>Сводные отчеты также предлагают набор статистической информации о контактах. Данная статистика предназначена только для обычных пользователей, которые выполнили вход не менее одного раза, а также имеют не менее одного контакта. Следовательно, как правило, вы не видите минимального количества контактов равное нулю. Благодаря данному поведению, если у пользователя отсутствуют контакты (но он считается активным из-за своей регистрации), можно увидеть значение &lt;пусто&gt; для некоторых полей статистики.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Отчеты на уровне пользователя</p></td>
<td><p>Dbanalyze /v /report:disk [/sqlserver:value]</p>
<p>В отличие от сводных отчетов, которые вычисляются на основе общего количества пользователей, эти отчеты характерны для определенного пользователя.</p></td>
</tr>
<tr class="even">
<td><p>Сводные отчеты по конференции</p></td>
<td><p>Dbanalyze /v /report:conf [/sqlserver:value]</p>
<p>В данном разделе представлена объединенная информация о сводной статистике конференции для пула, такая как количество активных конференций и общее число участников.</p></td>
</tr>
</tbody>
</table>


## Запуск анализатора использования пропускной способности

Анализатор использования полосы пропускания – это средство, которое создает отчеты о различных аспектах использования пропускной способности каналов глобальной сети с помощью конечных точек объединенных коммуникаций в корпоративной сети. Эти отчеты можно использовать для анализа текущей схемы использования пропускной способности, а также при планировании емкости пропускной способности. Оно также позволяет просматривать пропускную способность, назначенную различным каналам.

Это средство предоставляет следующие возможности:

  - создание определенных отчетов для использования аудио по всей сети;

  - позволяет более эффективно планировать емкость и распределять емкость пропускной способности, назначенную различным каналам.

Анализатор использования пропускной способности может создавать графические отчеты о пропускной способности и степени ее загрузки:

  - для всех каналов глобальной сети в корпоративной сети;

  - для выбранных каналов глобальной сети;

  - для каналов глобальной сети, емкость которых превышена;

  - для каналов глобальной сети, пропускная способность которых используется недостаточно;

  - для каналов глобальной сети, использование которых достигает критического уровня (то есть превышает 90 % пропускной способности канала глобальной сети);

  - для каналов глобальной сети, отфильтрованных по типу: каналы между сетевыми сайтами, каналы между областями и каналы внутри сайта;

  - с фильтрацией по области сети.

Документация для данного инструмента доступна в статье [Документация к инструментарию из набора ресурсов Lync Server 2013](https://technet.microsoft.com/ru-ru/library/jj945604\(v=ocs.15\)).

## См. также

#### Другие ресурсы

[Контрольный список еженедельных задач](lync-server-2013-operations-checklists.md)

