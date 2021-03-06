﻿---
title: 'Lync Server 2013: настройка магистрали без обхода сервера-посредника'
TOCTitle: Настройка магистрали без обхода сервера-посредника
ms:assetid: 3422e93e-7bd2-4470-968c-dc38345b18ca
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Gg425831(v=OCS.15)
ms:contentKeyID: 49309395
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Настройка магистрали без обхода сервера-посредника в Lync Server 2013

 

_**Дата изменения раздела:** 2013-02-24_

Если вы хотите настроить магистраль с обходом сервера-посредника, выполните эти действия. Сведения о настройке магистрали с включенным сервером-посредником см. в статье [Настройка магистрали с обходом сервера-посредника в Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md).

Конфигурация магистрали представляет собой набор параметров, применяемых к магистрали, которой назначается эта конфигурация. Определенная конфигурация магистрали может применяться глобально (ко всем магистралям, у которых нет особых настроек сайта или пула), к сайту или к пулу. Конфигурация магистрали уровня пула позволяет применить особую конфигурацию к отдельной магистрали.

## Настройка магистрали без обхода сервера-посредника

1.  Войдите на компьютер как член группы RTCUniversalServerAdmins или роли CsVoiceAdministrator, CsServerAdministrator или CsAdministrator. Дополнительные сведения см. в разделе [Делегирование разрешений на установку в Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Откройте окно браузера и введите URL-адрес для администрирования, чтобы открыть панель управления Lync Server. Дополнительные сведения о различных методах, которые можно использовать для запуска панели управления Lync Server см. в разделе [Открытие средств администрирования Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  В левой панели навигации щелкните **Маршрутизация голосовой связи** и **Настройка магистрали** .

4.  На странице **Настройка магистрали** воспользуйтесь одним из следующих методов:
    
      - Дважды щелкните имеющуюся магистраль (например, **Глобальную** ), чтобы открыть окно **Изменение настройки магистрали** .
    
      - Нажмите **Создать** и выберите область для новой конфигурации магистрали:
        
          - **Магистральная линия связи сайта**. В окне **Выбор сайта** выберите сайт для этой конфигурации магистрали, затем нажмите кнопку **ОК** . Обратите внимание, что сайт, для которого уже создана конфигурация магистрали, не появляется в окне **Выбор сайта** . Эта конфигурация будет применяться ко всем магистралям на сайте.
        
          - **Магистральная линия связи пула**. В окне **Выбор службы** выберите название магистрали, к которой применяется эта конфигурация, затем нажмите кнопку **ОК** . Это может быть корневая магистраль или любые дополнительные магистрали, заданные в средстве определения топологий. Обратите внимание, что магистраль, для которой уже создана конфигурация, не появляется в окне **Выбор службы** .
    
    > [!NOTE]  
    > Выбранную область конфигурации магистрали нельзя изменить.<br />    Поле <strong>Название</strong> заполняется названием связанного с конфигурацией магистрали сайта или службы. Изменить его нельзя.

5.  Выберите один из следующих вариантов для **Уровня поддержки шифрования** :
    
      - **Обязательный :** должно использоваться шифрование по протоколу SRTP для защиты трафика между сервером-посредником и шлюзом или УАТС.
    
      - **Необязательно :** SRTP-шифрование будет использоваться, если ее поддерживает поставщик или возможности оборудования.
    
      - **Не поддерживается :** SRTP-шифрование не поддерживается поставщиком или оборудованием, и потому использоваться не будет.

6.  Убедитесь, что флажок **Разрешить обход мультимедиа** снят.

7.  Установите флажок **Централизованная обработка мультимедиа** , если существует известная точка терминирования медиаданных (например, шлюз телефонной сети общего пользования (ТСОП), где у точки терминирования такой же IP-адрес, как и у точки терминирования сигналов). Снимите этот флажок, если в магистрали нет известной точки терминирования медиаданных.

8.  Если узел магистрали поддерживает получение запросов SIP REFER от посредник, установите флажок **Разрешить отправку ссылки шлюзу** .

9.  (Необязательно) Чтобы включить маршрутизацию между магистральными линиями связи, сопоставьте и настройте записи режима работы с ТСОП для этой конфигурации магистральной линии связи. Записи режима работы с ТСОП, связанные с этой конфигурацией магистральной линии связи, будут применены ко всем входящим вызовам через магистральную линию связи, которые начинаются за пределами конечной точки Lync. Чтобы управлять записями режима работы с ТСОП, связанными с конфигурацией магистральной линии связи, используйте один из приведенных ниже методов.
    
      - Чтобы выбрать одну или несколько записей из списка записей режима работы с ТСОП, доступных в развертывании корпоративной голосовой связи, щелкните пункт **Выбрать** . Выделите записи, которые следует связать с этой конфигурацией магистральной линии связи, и нажмите кнопку **ОК** .
    
      - Чтобы удалить запись режима работы с ТСОП из этой конфигурации магистральной линии связи, выберите эту запись и щелкните **Удалить** .
    
      - Чтобы определить новую запись режима работы с ТСОП и сопоставить ее с этой конфигурацией магистральной линии связи, выполните следующие действия.
        
        1.  Щелкните **Создать** .
        
        2.  В поле **Имя** укажите уникальное описательное имя для записи.
            
            > [!NOTE]  
            > Имя записи режима работы с ТСОП должно быть уникальным в пределах развертывания корпоративной голосовой связи. После сохранения записи поле <strong>Имя</strong> становится недоступным для изменения.        
        3.  Используйте один из следующих методов для сопоставления и настройки маршрутов для этой записи режима работы с ТСОП:
            
              - Чтобы выбрать один или более маршрутов из списка всех доступных маршрутов в развертывании корпоративной голосовой связи, щелкните **Выбрать** . Выделите маршруты, которые требуется сопоставить с этой записью режима работы с ТСОП, и нажмите кнопку **ОК** .
            
              - Чтобы удалить маршрут из записи режима работы с ТСОП, выберите этот маршрут и щелкните **Удалить** .
            
              - Чтобы определить новый маршрут и сопоставить его с этой записью режима работы с ТСОП, щелкните **Создать** . Дополнительные сведения см. в разделе [Создание голосового маршрута в Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Чтобы изменить маршрут, сопоставленный с этой записью режима работы с ТСОП, выберите данный маршрут и щелкните **Подробнее** . Дополнительные сведения см. в разделе [Изменение голосового маршрута в Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        4.  Нажмите кнопку **ОК** .
    
      - Чтобы изменить запись режима работы с ТСОП, уже сопоставленную с этой настройкой магистральной линии связи, выполните следующие действия:
        
        1.  Выберите запись режима работы с ТСОП, которую требуется изменить, и щелкните **Подробнее** .
        
        2.  Используйте один из следующих методов для сопоставления и настройки маршрутов для этой записи режима работы с ТСОП:
            
              - Чтобы выбрать один или более маршрутов из списка всех доступных маршрутов в развертывании корпоративной голосовой связи, щелкните **Выбрать** . Выделите маршруты, которые требуется сопоставить с этой записью режима работы с ТСОП, и нажмите кнопку **ОК** .
            
              - Чтобы удалить маршрут из записи режима работы с ТСОП, выберите этот маршрут и щелкните **Удалить** .
            
              - Чтобы определить новый маршрут и сопоставить его с этой записью режима работы с ТСОП, щелкните **Создать** . Дополнительные сведения см. в разделе [Создание голосового маршрута в Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Чтобы изменить маршрут, сопоставленный с этой записью режима работы с ТСОП, выберите данный маршрут и щелкните **Подробнее** . Дополнительные сведения см. в разделе [Изменение голосового маршрута в Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        3.  Нажмите кнопку **ОК** .
    
    > [!IMPORTANT]  
    > Важно, чтобы сопоставление записи режима работы с ТСОП выполнялось в соответствии с одноранговым посредник, сопоставленным с настраиваемой магистральной линией связи. Если одноранговым посредник является шлюз ТСОП или пограничный контроллер сеансов (SBC), настоятельно рекомендуется, чтобы настройка магистральной линии связи не сопоставлялась с записью режима работы с ТСОП, для которой указан маршрут к конечной телефонной сети ТСОП или каким-либо другим подчиненным системам, подключенным через Lync Server.

10. Измените расположение записей режима работы с ТСОП, чтобы обеспечить оптимальную производительность. Чтобы изменить расположение записи в списке, выберите соответствующую запись режима работы с ТСОП и щелкните стрелку вверх или стрелку вниз.
    
    > [!IMPORTANT]  
    > Порядок расположения записей режима работы с ТСОП в списке является важным. Lync Server просматривает этот список в направлении сверху вниз.

11. Установите флажок **Разрешить блокирование RTP** , чтобы разрешить обход сервера-посредника для клиентов, находящихся за устройством NAT (преобразование сетевых адресов) или брандмауэром, и пограничного контроллера сеансов, поддерживающего блокирование.

12. **Включить журнал переадресации звонков** следует выбрать, чтобы включить отправку информации журнала вызовов одноранговому шлюзу посредник.

13. Установите флажок **Включить данные переадресации P-Asserted-Identity** , чтобы разрешить переадресацию информации PAI вызывающей стороны из сервера посредник в шлюз (и наоборот), если такая информация имеется.

14. Чтобы включить быструю отработку отказа, выберите **Включить таймер отработки отказа внешней маршрутизации** . Шлюз, связанный с данной магистралью, может отправить уведомление об обработке исходящего вызова в течение 10 секунд. Перенаправление на другую магистраль происходит, если сервер посредник не получает это уведомление. Для сетей с высокой задержкой, которая может увеличить время ответа, или для шлюзов, время отклика которых превышает 10 секунд, быстрая отработка отказа должна быть отключена.

15. (Необязательно) Сопоставьте и настройте **правила трансляции вызывающего номера** для магистральной линии связи. Эти правила применяются к вызывающим номерам для исходящих вызовов
    
      - Чтобы выбрать одно или несколько правил из списка правил трансляции, доступных в развертывании корпоративной голосовой связи, щелкните **Выбрать** . В окне **Выбор правил трансляции** выберите правила, которые требуется сопоставить с магистральной линией связи, а затем нажмите кнопку **ОК** .
    
      - Чтобы определить новое правило преобразования и сопоставить его с магистральной линией связи, щелкните **Создать** . Дополнительные сведения об определении нового правила см. в разделе [Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md) в документации по развертыванию.
    
      - Чтобы изменить правило преобразования, уже сопоставленное с магистральной линией связи, щелкните имя правила, а затем выберите **Подробнее** . Дополнительные сведения см. в разделе [Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md) в документации по развертыванию.
    
      - Чтобы скопировать существующее правило преобразования и использовать его в качестве отправной точки для определения нового правила, щелкните имя этого правила, щелкните **Копировать** и **Вставить** . Дополнительные сведения см. в разделе [Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Чтобы удалить правило преобразования из магистральной линии связи, выделите имя этого правила, а затем щелкните **Удалить** .
    
    > [!security]  
    > Не сопоставляйте правила преобразования с магистральной линией связи, если вы уже настроили их для связанной одноранговой магистральной линии связи, поскольку эти два правила могут конфликтовать друг с другом.

16. (Необязательно) Сопоставьте и настройте **правила трансляции набранного номера** для магистральной линии связи. Эти правила применяются к вызываемым номерам для исходящих вызовов.
    
      - Чтобы выбрать одно или несколько правил из списка правил трансляции, доступных в развертывании корпоративной голосовой связи, щелкните **Выбрать** . В окне **Выбор правил трансляции** выберите правила, которые требуется сопоставить с магистральной линией связи, а затем нажмите кнопку **ОК** .
    
      - Чтобы определить новое правило преобразования и сопоставить его с магистральной линией связи, щелкните **Создать** . Дополнительные сведения об определении нового правила см. в разделе [Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md) в документации по развертыванию.
    
      - Чтобы изменить правило преобразования, уже сопоставленное с магистральной линией связи, щелкните имя правила, а затем выберите **Подробнее** . Дополнительные сведения см. в разделе [Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md) в документации по развертыванию.
    
      - Чтобы скопировать существующее правило преобразования и использовать его в качестве отправной точки для определения нового правила, щелкните имя этого правила, щелкните **Копировать** и **Вставить** . Дополнительные сведения см. в разделе [Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Чтобы удалить правило преобразования из магистральной линии связи, выделите имя этого правила, а затем щелкните **Удалить** .
    
    > [!Caution]  
    > Не сопоставляйте правила преобразования с магистральной линией связи, если вы уже настроили их для связанной одноранговой магистральной линии связи, поскольку эти два правила могут конфликтовать друг с другом.

17. Правила трансляции линии связи должны быть выстроены в правильном порядке. Чтобы изменить положение правила в списке, выделите имя правила и нажмите кнопку со стрелкой вверх или вниз.
    
    > [!IMPORTANT]  
    > Lync Server просматривает список правил трансляции сверху вниз и использует первое правило, совпадающее с набранным номером. Если магистраль настроена так, что набранный номер может соответствовать нескольким правилам, то более строгие правила должны предшествовать менее строгим. Например, если вы добавили правило трансляции, совпадающее с любым 11-значным номером и правило, совпадающее с 11-значным номером, начинающимся на +1425, то первое правило должно располагаться <em>ниже</em> второго, более строгого правила.

18. После завершения настройки магистрали нажмите **ОК** .

19. На странице **Настройка магистрали** нажмите **Фиксировать** и затем **Фиксировать все** .
    
    > [!NOTE]  
    > После создания или изменения конфигурации магистрали следует выполнить команду <strong>Сохранить все</strong> , чтобы опубликовать изменения конфигурации. Дополнительные сведения см. в разделе <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Публикация ожидающих изменений в конфигурации маршрутизации голосовой связи в Lync Server 2013</a> в документации по применению.

## См. также

#### Задачи

[Настройка магистрали с обходом сервера-посредника в Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  

#### Другие ресурсы

[Определение правил преобразования в Lync Server 2013](lync-server-2013-defining-translation-rules.md)

