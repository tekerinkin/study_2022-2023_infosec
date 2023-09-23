---
## Front matter
lang: ru-RU
title: Лабораторная работа №3
subtitle: Дискреционное разграничение прав в Linux. Два пользователя
author:
  - Шестаков Д. С.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 23 сентября 2023

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Шестаков Дмитрий Сергеевич
  * студент группы НКНбд-01-20
  * Российский университет дружбы народов
  * [dmshestakov@icloud.com](mailto:dmshestakov@icloud.com)

:::
::::::::::::::

# Вводная часть

## Объект и предмет исследования

- Rocky Linux
- Bash
- Дискреционное разграничение прав

## Цели и задачи

- Получение практических навыков работы в консоли с атрибутами файлов для групп пользователей.

# Ход работы

## Выполнение работы

В установленной операционной системе создали две учетные записи: guest и guset2

```bash
useradd guest
passwd guest

useradd guest2
passwd guest2
```

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="70%"}
![Создание пользователей](../report/image/1.png){#fig:001 width=70%}
:::
::::::::::::::

## Выполнение работы

Добавили пользователя guest2 в guest

```bash
gpaswwd -a guest2 guest
```

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="70%"}
![Добавление пользователя в группу](../report/image/2.png){#fig:002 width=70%}
:::
::::::::::::::

## Выполнение работы

Осуществили вход в систему от двух разных пользователей:

```bash
su - guest
su - guest2
```

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="70%"}
![Логин в guest](../report/image/3.png){#fig:003 width=70%}
:::
::::::::::::::

## Выполнение работы

Определили директорию, в которой находится каждый из пользователей, командой ```pwd```

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="50%"}
![Определение пути guest2](../report/image/4.png){#fig:004 width=70%}
:::
::: {.column width = "50%"}
![Определение пути guest](../report/image/5.png){#fig:005 width=70%}
:::
::::::::::::::

## Выполнение работы

Сравнили выводы команд ```groups```, ```id -G``` и ```id -Gn``` для обоих пользователей. Заметили, что команды ```groups```, ```id -Gn```
выводят названия групп, а команда ```id -G``` их uid.

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="50%"}
![Id guest2](../report/image/6.png){#fig:006 width=70%}
:::
::: {.column width = "50%"}
![Id guest](../report/image/7.png){#fig:007 width=70%}
:::
::::::::::::::

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="50%"}
![Groups, id -G guest](../report/image/8.png){#fig:008 width=70%}
:::
::: {.column width = "50%"}
![Groups, id -G guest2](../report/image/9.png){#fig:009 width=70%}
:::
::::::::::::::

## Выполнение работы

Просмотрели файл /etc/group командой ```cat /etc/group | grep guest```

## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="50%"}
![Файл /etc/group (guest2)](../report/image/10.png){#fig:010 width=70%}
:::
::: {.column width = "50%"}
![Файл /etc/group (guest)](../report/image/11.png){#fig:011 width=70%}
:::
::::::::::::::

## Выполнение работы

От имени пользователя guest2 зарегистрировали пользователя в группе guest командой ```newgrp guest```


## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="70%"}
![Регистрация guest2](../report/image/12.png){#fig:012 width=70%}
:::
::::::::::::::

## Выполнение работы

От имени пользователя guest изменили права директории /home/guest, разрешив все действия для пользователей группы

```bash
chmod g+rwx /home/guest
```


## Выполнение работы

От имени пользователя guest сняли все атрибуты с директории /home/guest/dir1

```bash
chmod 00 dir1
```

## Выполнение работы

Заполнили таблицу возможных действий с различными атрибутами директории


## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="70%"}
![Таблица](../report/image/13.png){#fig:013 width=70%}
:::
::::::::::::::

## Выполнение работы

Заполнили таблицу минимально неободимых атрибутов для определенных действий


## Выполнение работы

:::::::::::::: {.columns align=center}
::: {.column width="70%"}
![Таблица 2](../report/image/14.png){#fig:014 width=70%}
:::
::::::::::::::


## Вывод

Получили практические навыки работы с атрибутами директорий и файлов в группе в консоли.
