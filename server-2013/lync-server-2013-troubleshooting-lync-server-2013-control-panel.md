﻿---
title: Устранение неполадок с панелью управления в Lync Server 2013
TOCTitle: Устранение неполадок с панелью управления в Lync Server 2013
ms:assetid: 54e7ab57-34ce-4a07-bcc9-643379eb4eb7
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg195689(v=OCS.15)
ms:contentKeyID: 49309801
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Устранение неполадок с панелью управления в Lync Server 2013

 

_**Дата изменения раздела:** 2016-12-08_

В этом разделе содержатся сведения и процедуры, помогающие устранять неполадки доступа к панели управления Lync Server 2013.

## Требования к Интернет-браузеру

Для панели управления Lync Server требуется установка для браузеров Microsoft Silverlight версии не ниже 4.0.50524.0. Если браузер Silverlight не установлен или имеет более раннюю версию, то следуйте инструкциям в сообщении для установки необходимой версии.

> [!NOTE]  
> Другие требования к программному обеспечению для панели управления Lync Server относятся к операционной системе, в которой может быть установлена панель управления Lync Server и все прочие средства администрирования сервера Lync Server 2013. Подробные сведения см. в разделе <a href="lync-server-2013-server-and-tools-operating-system-support.md">Поддержка сервера и средств в операционной системе в Lync Server 2013</a> документации по поддержке.

Если ваш Интернет-браузер блокирует установку Silverlight по соображениям безопасности, добавьте URL-адрес, который открывает панель управления Lync Server, в список доверенных сайтов. В параметрах безопасности Internet Explorer убедитесь, что параметр **Запускать элементы ActiveX и подключаемые модуливключен**. Подробные сведения см. на странице [http://go.microsoft.com/fwlink/?linkid=214060\&clcid=0x419](http://go.microsoft.com/fwlink/?linkid=214060%26clcid=0x419). Кроме того, убедитесь, что браузер настроен для использования SSL 3.0.

Если Интернет-браузер настроен для использования прокси-сервера, то убедитесь, что задан обход прокси-сервера для сайтов, которые автоматически определяются как внутренние сайты. Можно также добавить этот адрес в список исключений браузера в параметрах конфигурации прокси-сервера.

## Требования к записи DNS и к сертификату для URL-адреса административного доступа

Если для доступа к панели управления Lync Server настроен простой URL-адрес, то должна быть также настроена статическая запись ресурса узла (запись А) службы доменных имен (DNS) и сертификат, необходимый для использования этого URL-адреса административного доступа. Убедитесь, что при изменении этого базового URL-адреса в любое время это изменение отражается в соответствующей записи DNS ив сертификате, и что для регистрации этого изменения командлет *Enable-CsComputer* был выполнен в каждом сервере Директор и сервере переднего плана. Подробные сведения см. в следующих разделах документации по планированию.

  - [Планирование простых URL-адресов в Lync Server 2013](lync-server-2013-planning-for-simple-urls.md)

  - [Требования DNS для простых URL-адресов в Lync Server 2013](lync-server-2013-dns-requirements-for-simple-urls.md)

  - [Требования к сертификатам для внутренних серверов в Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md)

Пошаговые процедуры по настройке URL-адреса административного доступа см. в разделе [Изменить или настроить простые URL-адреса в Lync Server 2013](lync-server-2013-edit-or-configure-simple-urls.md) документации по развертыванию.

> [!NOTE]  
> Если на веб-сервере имеется несколько сетевых адаптеров, то необходимо вручную настроить DNS для каждого дополнительного адаптера, чтобы разрешение DNS работало должным образом.

## Требования к службам IIS

Панель управления Lync Server является одним из компонентов сервера Lync Server 2013, которому требуются службы Службы IIS. В частности, следует убедиться, что включены функции перенаправления HTTP и проверки подлинности Windows, и что служба веб-публикаций (W3SVC) выполняется.

## Зависимость от службы веб-публикаций (службы Windows)

Если служба веб-публикаций остановлена, то нельзя получить доступ к панели управления Lync Server. Необходимо перезапустить эту службу с помощью консоли управления (MMC) служб Windows.

**Запуск службы веб-публикаций**

1.  Войдите в компьютер, на котором установлена служба веб-публикаций как часть служб Службы IIS.

2.  Нажмите кнопку **Пуск**, а затем последовательно выберите пункты **Администрирование** и **Службы**.

3.  Щелкните правой кнопкой мыши **службу веб-публикаций** и выберите команду **Пуск**.

## Режим пула приложений

Настройте службы IIS таким образом, чтобы пул приложений CsManagementAppPool использовал учетную запись сетевой службы в качестве удостоверения своей модели процесса.

## Пользовательские права и разрешения

Необходимо входить в панель управления Lync Server либо с помощью учетной записи домена, которая является членом группы CsAdministrator, либо с помощью учетной записи, которой делегированы пользовательские права и разрешения. Нельзя войти в панель управления Lync Server с помощью локальной учетной записи компьютера. Подробные сведения о делегировании административных задач с помощью управления доступом на основе ролей (RBAC) см. в разделе [Планирование контроля доступа на основе ролей в Lync Server 2013](lync-server-2013-planning-for-role-based-access-control.md) документации по планированию.

При использовании простого URL-адреса для доступа к панели управления Lync Server убедитесь, что веб-серверы добавлены в группы RTCUniversalServerAdmins и RTCUniversalUserAdmins.

## См. также

#### Концепции

[Средства администрирования Lync Server 2013](lync-server-2013-lync-server-administrative-tools.md)

