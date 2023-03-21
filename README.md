# lab03

## Подготовка

```
$ sudo apt install git
```

Устанвливаем имя пользователя и email

```
$ git config --global user.name "Masha"
$ git config --global user.email "mkkazakova@yandex.ru"
```

В гитхабе создаем свой токен

Создаём директорию lab-03. И заходим туда

```
$ mkdir lab-03
$ cd ~/lab-03
```

Создаём репозиторий lab03

```
echo "# lab03" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/mkkazakova/lab03.git
git push -u origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)

![image](https://user-images.githubusercontent.com/125077130/226595680-1be98e53-7a46-4c33-850f-89a2f53de236.png)

## 1 часть

Создаём директорию formatter_lib. Заходим туда. Создаём файл CMakeLists.txt

```
$ mkdir formatter_lib
$ cd formatter_lib - Меняем директорию
$ cat >> CMakeLists.txt << EOF
```
Выскочит значок >. Написать EOF

Редактируем файл

```
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter)

add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

Добавляем файлы formatter.cpp и formatter.h в папку "formatter_lib" 
(взять их можно по ссылке - https://github.com/tp-labs/lab03/tree/master/formatter_lib)

```
$ wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.cpp
$ wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.h
```

Устанавливаем пакет cmake

```
$ sudo apt install cmake 
```

Проверяем работоспособность

```
$ cmake -H. -B_build
$ cmake --build _build
```

Всё пушим и коммитим

```
$ cd ..
$ git add formatter_lib
$ git commit -m "formatter"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)

## 2 часть

Создаём директорию formatter_ex_lib. Заходим туда. Создаём файл CMakeLists.txt

```
$ mkdir formatter_ex_lib
$ cd formatter_ex_lib
$ cat >> CMakeLists.txt << EOF
```
Выскочит значок >. Написать EOF

Редактируем файл

```
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter_ex)

add_library(formatter_ex STATIC formatter_ex.cpp)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter)
target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(formatter_ex formatter)
```

Добавляем файлы formatter_ex.cpp и formatter_ex.h в папку "formatter_ex_lib" 
(взять их можно по ссылке - https://github.com/tp-labs/lab03/tree/master/formatter_ex_lib)

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_ex_lib/formatter_ex.cpp
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_ex_lib/formatter_ex.h
```

Проверяем работоспособность

```
$ cmake -H. -B_build
$ cmake --build _build
```

Всё пушим и коммитим

```
$ cd ..
$ git add formatter_ex_lib
$ git commit -m "formatter_ex"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)

## 3 часть

### Для hello world

Создаём директорию  hello_world_application. Заходим туда. Создаём файл CMakeLists.txt 

```
$ mkdir hello_world_application
$ cd hello_world_application
$ cat >> CMakeLists.txt << EOF
```

Выскочит значок >. Написать EOF

Редактируем файл

```
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(hello_world_example)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)
add_executable(example hello_world.cpp)

target_link_libraries(example formatter_ex)
```

Добавляем файл hello_world.cpp в папку "hello_world_application" 
(взять их можно по ссылке - https://github.com/tp-labs/lab03/tree/master/hello_world_application)

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/hello_world_application/hello_world.cpp
```

Проверяем работоспособность

```
$ cmake -H. -B_build
$ cmake --build _build
```

Запускаем программу

```
$ cmake --build _build --target example
$ ./_build/example
```

Выводится: hello world

Всё пушим и коммитим

```
$ cd ..
$ git add hello_world_application
$ git commit -m "hello world"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)

### Для solver

Создаём директорию  solver_lib. Заходим туда. Создаём файл CMakeLists.txt 

```
$ mkdir solver_lib
$ cd solver_lib - Меняем директорию
$ cat >> CMakeLists.txt << EOF
```
Выскочит значок >. Написать EOF

Редактируем файл

```
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_lib)

add_library(solver_lib STATIC solver.cpp)
target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

Добавляем файлы solver.cpp и solver.h в папку "solver_lib" 
(взять их можно по ссылке - https://github.com/tp-labs/lab03/tree/master/solver_lib)

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/solver_lib/solver.cpp
wget https://raw.githubusercontent.com/tp-labs/lab03/master/solver_lib/solver.h
```

В файле solver.cpp допущена ошибка. Исправленный код:

```
$ nano solver.cpp

#include "solver.h"

#include <stdexcept>
#include <math.h>

void solve(float a, float b, float c, float& x1, float& x2)
{
    float d = (b * b) - (4 * a * c);

    if (d < 0)
    {
        throw std::logic_error{"error: discriminant < 0"};
    }

    x1 = (-b - std::sqrt(d)) / (2 * a);
    x2 = (-b + std::sqrt(d)) / (2 * a);
}
```

Проверяем работоспособность

```
$ cmake -H. -B_build
$ cmake --build _build
```

Всё пушим и коммитим

```
$ cd ..
$ git add solver_lib
$ git commit -m "solvers_lib"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)

Создаём директорию  solver_application. Заходим туда. Создаём файл CMakeLists.txt

```
$ mkdir solver_application
$ cd solver_application
$ cat >> CMakeLists.txt << EOF
```

Выскочит значок >. Написать EOF

Редактируем файл

```
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_example)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib ${CMAKE_CURRENT_BINARY_DIR}/solver_lib)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)

add_executable(example equation.cpp)

target_link_libraries(example solver_lib formatter_ex)
```

Добавляем файл equation.cpp в папку "solver_application"

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/solver_application/equation.cpp
```

Проверяем работоспособность

```
$ cmake -H. -B_build
$ cmake --build _build
```

Запускаем программу

```
$ cmake --build _build --target example
$ ./_build/example
```

Всё пушим и коммитим

```
$ cd ..
$ git add solver_application
$ git commit -m "solver"
$ git push origin master
```

Далее требуется ввести логин (своё имя на GitHub), затем пароль (свой токен)


## Скрины

I

![image](https://user-images.githubusercontent.com/125077130/226595893-f5ac8830-7549-4dae-9f64-3e3fda437b5a.png)

![image](https://user-images.githubusercontent.com/125077130/226595925-8e46f9ef-89b8-4878-a1fb-21e6371e0766.png)

II

![image](https://user-images.githubusercontent.com/125077130/226595962-d131ff1c-5002-4f77-aba9-7673c9379d87.png)

![image](https://user-images.githubusercontent.com/125077130/226596013-bf215dd2-3066-4ba7-a300-6a076948111c.png)

III

![image](https://user-images.githubusercontent.com/125077130/226596085-3143dc24-6506-4754-ad46-338f2db087b6.png)

![image](https://user-images.githubusercontent.com/125077130/226596137-41b3c31a-ada6-4e94-898c-d563ae51e1c2.png)

![image](https://user-images.githubusercontent.com/125077130/226596165-5388bbe1-e99c-4d02-aac4-1ba9666d9a58.png)

![image](https://user-images.githubusercontent.com/125077130/226596188-55f93fcc-ea8e-48d9-acbe-425c983a6a28.png)

![image](https://user-images.githubusercontent.com/125077130/226596222-da5855d5-b8d5-41a9-a250-16c21aa69163.png)

![image](https://user-images.githubusercontent.com/125077130/226596265-00df82d4-1834-40be-9b15-3fae3807522b.png)

![image](https://user-images.githubusercontent.com/125077130/226596314-32b9ef6c-55d2-4d0a-baa5-50bfadd2de22.png)

