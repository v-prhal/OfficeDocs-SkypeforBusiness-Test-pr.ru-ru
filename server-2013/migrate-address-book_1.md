﻿---
title: Перенос адресной книги
TOCTitle: Перенос адресной книги
ms:assetid: b6e000ce-8b2e-460c-8a8b-000254b9d778
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ205198(v=OCS.15)
ms:contentKeyID: 49310937
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Перенос адресной книги

 

_**Дата изменения раздела:** 2012-10-02_

**Перенос настроенных правил нормализации адресной книги**

1.  Найдите файл Company\_Phone\_Number\_Normalization\_Rules.txt в корне общей папки адресной книги и скопируйте его в корень общей папки адресной книги в пилотном пуле Lync Server 2013.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398412.note(OCS.15).gif" title="note" alt="note" />Примечание</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Образцы правил нормализации адресной книги установлены в каталоге, содержащем файлы веб-компонента службы адресной книги. Путь – <strong>$installedDriveLetter:\Program Files\Microsoft Lync Server 2013\Web Components\Address Book Files\Files\ Sample_Company_Phone_Number_Normalization_Rules.txt,</strong>. Этот файл можно скопировать в корневой каталог общей папки адресной книги и переименовать в <strong>Company_Phone_Number_Normalization_Rules.txt</strong>. Например, для общей адресной книги на сервере <strong>$serverX</strong> путь будет иметь следующий вид: <strong>\\$serverX \LyncFileShare\2-WebServices-1\ABFiles</strong>.</td>
    </tr>
    </tbody>
    </table>


2.  Откройте файл Company\_Phone\_Number\_Normalization\_Rules.txt с помощью текстового редактора, например Блокнота.

3.  Некоторые типы записей будут работать в Lync Server 2013 неправильно. Просмотрите файл, чтобы найти записи такого типа, измените их требуемым образом и сохраните изменения в общей папке адресной книги в пилотном пуле.
    
    Строки, содержащие обязательный пробел или знак пунктуации, приведут к сбою правила нормализации, поскольку эти символы удаляются из строки при ее вводе в правило. Если у вас есть строки с обязательным пробелом или знаком пунктуации, их нужно изменить. Например, следующая строка приведет к сбою правила нормализации.
    
        \s*\(\s*\d\d\d\s*\)\s*\-\s*\d\d\d\s*\-\s*\d\d\d\d
    
    Следующая строка не приведет к сбою правила нормализации.
    
        \s*\(?\s*\d\d\d\s*\)?\s*\-?\s*\d\d\d\s*\-?\s*\d\d\d\d
