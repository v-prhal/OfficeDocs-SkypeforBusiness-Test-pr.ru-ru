﻿---
title: Конфигурация шлюза XMPP в Lync Server 2013
TOCTitle: Конфигурация шлюза XMPP в Lync Server 2013
ms:assetid: 00777a34-cc36-4992-9459-08c14543ef6b
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ687953(v=OCS.15)
ms:contentKeyID: 49887844
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Конфигурация шлюза XMPP в Lync Server 2013

 

_**Дата изменения раздела:** 2012-10-19_

При настройке политик для поддержки федеративных партнеров протокола XMPP эти политики применяются к пользователям федеративных доменов XMPP, но не к пользователям поставщиков услуг мгновенной передачи сообщений по протоколу SIP (например, Windows Live) или федеративных доменов SIP. Если нужно, чтобы пользователи могли добавлять контакты из федеративного домена XMPP и взаимодействовать с ними, для каждого такого домена настраивается федеративный партнер XMPP. После создания политик в качестве дополнительных задач нужно настроить сертификаты шлюза XMPP, развернуть шлюз XMPP Lync Server 2013, а затем обновить записи DNS для этого шлюза XMPP.

## Настройка сертификатов шлюза XMPP на пограничном сервере Lync Server 2013

1.  На пограничном сервере в мастере развертывания рядом с пунктом **Шаг 3. Запрос, установка или назначение сертификатов** нажмите кнопку **Повторный запуск** .
    

    > [!TIP]
    > Если развертывание пограничного сервера выполняется впервые, то вместо кнопки "Повторный запуск" будет отображаться кнопка "Запуск".



2.  На странице **Available Certificate Tasks** (Доступные задачи сертификатов) щелкните команду **Create a new certificate request** (Создать новый запрос сертификата).

3.  На странице **запроса сертификата** выберите пункт **External Edge Certificate** (Внешний сертификат пограничного сервера).

4.  На странице **Отложенный или немедленный запрос** установите флажок **Подготовить запрос сейчас, чтобы отправить его позже** .

5.  На странице **файла запроса сертификата** введите полный путь и имя файла, в который должен сохраняться запрос (например, c:\\cert\_exernal\_edge.cer).

6.  На странице **указания альтернативного шаблона сертификата** для использования шаблона, отличного от шаблона WebServer по умолчанию, установите флажок **Use alternative certificate template for the selected certification authority** (Использовать альтернативный шаблон сертификата для выбранного центра сертификации).

7.  На странице **настроек имени и безопасности** выполните следующие действия.
    
    1.  В поле **Понятное имя** введите отображаемое имя для сертификата.
    
    2.  В поле **Длина в битах** укажите длину в битах (обычно используется значение по умолчанию 2048).
    
    3.  Убедитесь, что флажок **Mark certificate private key as exportable** (Пометить закрытый ключ сертификата как экспортируемый) установлен.

8.  На странице **сведений об организации** укажите имя организации и подразделения (например, отделения или отдела).

9.  На странице **сведений о местоположении** укажите сведения о местоположении.

10. На странице **имени субъекта и альтернативных имен субъекта** отображаются сведения, автоматически заполненные мастером. Если требуются дополнительные альтернативные имена субъекта, то они указываются в следующих двух действиях.

11. На странице **параметров домена SIP в альтернативных именах субъекта (SAN)** установите флажок домена для добавления записи sip.\<домен\_sip\> в список альтернативных имен субъекта.

12. На странице **Настройка дополнительных альтернативных имен субъекта** укажите все необходимые дополнительные альтернативные имена субъекта.
    

    > [!TIP]
    > Если устанавливается прокси-сервер XMPP, то по умолчанию в записях SAN заполняется имя домена (например, contoso.com). Если требуются дополнительные записи, добавьте их сейчас.



13. На странице **сводки по запросу** просмотрите сведения о сертификате, которые будут использоваться для создания запроса.

14. После выполнения всех команд можно **Просмотреть журнал** или нажать кнопку **Далее** для продолжения.

15. На странице **Файл запроса сертификата** можно просмотреть файл сформированного запроса на подписание сертификата (CSR), нажав кнопку просмотра или выйдя из мастера сертификатов нажатием кнопки **Готово** .

16. Скопируйте файл запроса и отправьте его в ваш общедоступный центр сертификации.

17. После получения, импорта и назначения общедоступного сертификата необходимо остановить и перезапустить службы пограничного сервера. Это можно сделать, введя в консоли управления Lync Server следующую команду:
    
        Stop-CsWindowsService
    
        Start-CsWindowsService

## Настройка нового шлюза XMPP Lync Server 2013

1.  Откройте панель управления Lync Server.

2.  В левой панели навигации нажмите **Federation and External Access** (Федерация и внешний доступ), а затем выберите пункт **XMPP Federated Partners** (Федеративные партнеры XMPP).

3.  Чтобы создать новую конфигурацию, нажмите кнопку **Создать** .

4.  Задайте следующие параметры.

5.  **Основной домен**     (обязательно). Основной домен – это базовый домен партнера XMPP. Например, в качестве имени домена партнера XMPP можно указать **fabrikam.com**. Это обязательная запись.

6.  **Описание** .   В этом поле можно ввести заметки и другие полезные сведения для данной конкретной конфигурации. Эта запись не является обязательной.

7.  **Дополнительные домены** .   Это домены, которые являются частью домена партнера XMPP, и которые следует включить как часть разрешенного взаимодействия XMPP. Например, если в качестве основного домена указан **fabrikam.com**, то может потребоваться перечислить все остальные домены, входящие в домен fabrikam.com, с которыми будет осуществляться взаимодействие посредством XMPP.

8.  **Тип партнера** .   Параметр **Тип партнера** является обязательным. Необходимо выбрать один из указанных далее типов для описания контактов, которые могут добавляться. Можно выбрать один из следующих типов.
    
      - **Федеративный** .   Тип партнера **Федеративный** представляет наивысший уровень доверия между развертыванием Lync Server и партнером XMPP.  Этот тип партнера рекомендуется для федерации с серверами XMPP в одном предприятии или при наличии установленного бизнес-сотрудничества.  Контакты XMPP, указанные в федеративных партнерах, могут выполнять следующие действия.
        
        1.  Добавлять контакты Lync и просматривать их сведения о присутствии без необходимости экспресс-авторизации пользователем Lync.
        
        2.  Отправлять мгновенные сообщения контактам Lync независимо от того, были ли они добавлены пользователями Lync в свой список контактов.
        
        3.  Просматривать заметки о состоянии пользователя Lync.
    
      - **Общедоступный проверенный** .    **Общедоступный проверенный** партнер – это общедоступный поставщик XMPP, которому доверена проверка удостоверений своих пользователей.  Контакты XMPP в общедоступных проверенных сетях могут добавлять контакты Lync и просматривать их сведения о присутствии, а также отправлять им мгновенные сообщения без экспресс-авторизации пользователями Lync.  Контакты XMPP в общедоступных проверенных сетях никогда не видят заметки о состоянии пользователей Lync.  Эта установка не рекомендуется.
    
      - **Общедоступный непроверенный** .    **Общедоступный непроверенный** партнер – это общедоступный поставщик XMPP, которому не доверена проверка удостоверений своих пользователей.  Пользователи XMPP в общедоступных непроверенных сетях не могут взаимодействовать с пользователями Lync, пока пользователь Lync не выполнит их экспресс-авторизацию путем добавления их в список контактов.  Пользователи XMPP в общедоступных непроверенных сетях никогда не видят заметки о состоянии пользователей Lync.  Эта установка рекомендуется для федерации с общедоступными поставщиками XMPP, такими как Google Talk.

9.  **Тип подключения:** задает разные правила и параметры обратного вызова.
    
      - **Согласование TLS** .   Определяет правила согласования TLS. XMPP-служба может требовать TLS, может считать TLS необязательным элементом или указывать, что TLS не поддерживается. Выбор варианта "Необязательный" означает, что решение об обязательном согласовании принимается на стороне XMPP-службы. Все возможные значения и соответствующие сведения о согласовании SASL, TLS и обратного вызова – в том числе недопустимые и известные неправильные конфигурации – см. в статье [Параметры согласования для федеративных XMPP-партнеров в Lync Server 2013](lync-server-2013-negotiation-settings-for-xmpp-federated-partners.md)
        
          -   
            **Обязательный**     – служба XMPP требует согласование TLS.
        
          -   
            **Необязательный**     – служба XMPP указывает обязательность согласования TLS.
        
          -   
            **Не поддерживается**     – служба XMPP не поддерживает TLS.
    
      - **Согласование SASL** .   Задает правила согласования SASL. Служба XMPP может требовать SASL, может установить необязательность SASL, а также вы можете задать, что SASL не поддерживается. При выборе значения "Необязательно" решение об обязательности согласования будет принимать служба XMPP.
        
          -   
            **Обязательный**     – служба XMPP требует согласование SASL.
        
          -   
            **Необязательный**     – служба XMPP указывает обязательность согласования SASL.
        
          -   
            **Не поддерживается**     – служба XMPP не поддерживает SASL.
    
      - **Поддержка серверного согласования обратным вызовом** . Процесс серверного согласования обратным вызовом использует службу доменных имен (DNS) и полномочный сервер для проверки, пришел ли запрос от допустимого партнера XMPP. Для этого исходный сервер создает сообщение определенного типа с созданным ключом обратного вызова и ищет принимающий сервер в DNS. Затем исходный сервер отправляет этот ключ в XML-потоке в результат поиска в DNS, предположительно на принимающий сервер. После получения ключа в XML-потоке принимающий сервер не отвечает исходному серверу, а отправляет этот ключ на известный полномочный сервер. Полномочный сервер проверяет, является ли ключ допустимым. Если ключ недопустимый, то принимающий сервер не отвечает исходному серверу. Если ключ допустимый, то принимающий сервер информирует исходный сервер о допустимости удостоверения и ключа и о том, что можно начать беседу.
        
        **Согласование обратным вызовом** может иметь два следующих допустимых состояния.
        
          -   
            **True**     – сервер XMPP настроен для использования согласования обратным вызовом, если запрос будет получен от исходного сервера.
        
          -   
            **False**     – сервер XMPP не настроен для использования согласования обратным вызовом, и если запрос будет получен от исходного сервера, то он будет игнорироваться.

10. Нажмите кнопку **Commit** (Сохранить), чтобы сохранить изменения в политике на уровне сайта или пользователя.

## Обновление записей DNS для шлюза XMPP Lync Server 2013

1.  Чтобы настроить DNS для федерации XMPP, следует добавить во внешнюю DNS следующую запись SRV:\_xmpp-server.\_tcp.\<имя\_домена\>. Эта запись SRV будет преобразовываться в полное доменное имя пограничного доступа пограничного сервера со значением порта 5269.
