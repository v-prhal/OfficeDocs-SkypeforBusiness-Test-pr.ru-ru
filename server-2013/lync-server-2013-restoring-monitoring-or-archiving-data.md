﻿---
title: Восстановление данных архивации или мониторинга
TOCTitle: Восстановление данных архивации или мониторинга
ms:assetid: 60118526-13bb-4b03-803e-6ffae219d436
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Hh202175(v=OCS.15)
ms:contentKeyID: 52058242
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Восстановление данных архивации или мониторинга

 

_**Дата изменения раздела:** 2013-02-18_

Для восстановления работоспособности Lync Server после сбоя восстанавливать данные мониторинга и архивные данные не требуется. Однако если эти данные имеют критически важное значение для вашей организации, их может потребоваться восстановить после повторного создания баз данных.

В следующей процедуре описывается использование SQL Server Management Studio для восстановления данных мониторинга и архивных данных.

## Восстановление данных мониторинга и архивных данных из файла резервной копии

1.  Выполните вход на восстанавливаемый сервер с правами члена группы администраторов на локальном компьютере либо группы с аналогичными разрешениями.

2.  Откройте SQL Server Management Studio: нажмите кнопку **Пуск**, выберите **Все программы**, **Microsoft SQL Server 2012** или **Microsoft SQL Server 2008 R2**, а затем щелкните пункт **SQL Server Management Studio**.

3.  В окне **Подключение к серверу** подключитесь к экземпляру SQL Server, указав хотя бы имя сервера и сведения для аутентификации.

4.  В **обозревателе объектов** щелкните элемент **Базы данных** правой кнопкой мыши и выберите пункт **Восстановить базу данных**.

5.  В области **Выбор страницы** щелкните элемент **Общие**, а затем в поле **Целевая база данных** выберите имя базы данных следующим образом:
    
      - Для базы данных архивации выберите **LcsLog**.
    
      - Для базы данных регистрации вызовов (CDR) выберите **LcsCDR**.
    
      - Для базы данных качества взаимодействия (QoE) выберите **QoEMetrics**.

6.  Щелкните элемент **С устройства**.

7.  В области **Выберите резервные наборы данных для восстановления** щелкните файл резервной копии и нажмите кнопку **Восстановить**.

8.  В области **Выбор страницы** щелкните элемент **Параметры**, убедитесь, что путь к файлу данных и путь к журналу указаны в правильной папке, а затем нажмите кнопку **ОК**.

## Проверка правильности списков управления доступом (ACL)

1.  Разверните узел **Базы данных**, разверните базу данных архивации или мониторинга, разверните узел **Безопасность** и затем узел **Пользователи**.

2.  Убедитесь, что группа доменов RTCComponentUniversalServices существует в качестве пользователя.

3.  Если RTCComponentUniversalServices в области **Пользователи** отсутствует, выполните следующие действия:
    
    1.  Щелкните правой кнопкой мыши элемент **Пользователи** и выберите пункт **Создать пользователя**.
    
    2.  В поле **Имя для входа** введите имя отсутствующей группы — RTCComponentUniversalServices.
    
    3.  В области **Членство в роли базы данных** выберите разрешение **ServerRole** и нажмите кнопку **ОК**.
    
    > [!NOTE]  
    > Перезапуск службы архивации или мониторинга не требуется.
