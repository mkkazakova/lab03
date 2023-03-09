# lab03

## Подготовка к лабе

```
$ sudo apt install git
```

Устанвливаем имя пользователя и email

```
$ git config --global user.name "Masha"
$ git config --global user.email "mkkazakova@yandex.ru"
```

Создаём директорию. Затем миняем директорию.

$ mkdir lab-03
$ cd ~/lab-03

![image](https://user-images.githubusercontent.com/125077130/224116880-0ea5f11f-83f9-4ae5-80bd-2996de6f5b05.png)

В гитхабе создаем свой токен 

Далее действуем по инструкции, которая дана после создания репозитория:

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

## I Часть 

Создаём директорию formatter_lib и заходим в неё

```
$ mkdir formatter_lib
$ cd formatter_lib 
```

Создаём пустой файл CMakeLists.txt
```
$ cat >> CMakeLists.txt << EOF
```

Выскакивает значок " > " Записываем туда EOF. Затем редактируем этот файл:

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

ctrl+O, enter

>cmake_minimum_required указывает подходящую минимальную версию Cmake

>set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake
>(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)

>project(formatter) создает проект formatter, к которому можно подключать библиотеки, исполняемы файлы и т.д.

>add_library(formatter STATIC formatter.cpp) создает статическую (STATIC) библиотеку (с именем formatter) из указываемых файлов (formatter.cpp)

>target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}) связывает библиотеку formatter и CMAKE_CURRENT_SOURCE_DIR

Добавляем файлы formatter.cpp и formatter.h в папку "formatter_lib" 

```
$ wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.cpp
$ wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_lib/formatter.h
```

Устанавливаем пакет cmake:

```
$ sudo apt install cmake
```

Проверяем работоспособность:

```
$ cmake -H. -B_build
$ cmake --build _build
```


## II Часть

Выходим из прошлой директории (возвращаемся в lab-03). Создаём в папке lab-03 директорию formatter_ex_lib. Заходим туда:

```
$ cd .. 
$ mkdir formatter_ex_lib
$ cd formatter_ex_lib
```

Создаём пустой файл CMakeLists.txt

```
$ cat >> CMakeLists.txt << EOF
```

Выскакивает значок " > " Записываем туда EOF. Затем редактируем этот файл:

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

>cmake_minimum_required указывает подходящую минимальную версию Cmake

>set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake
>(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)

>project(formatter_ex) создает проект formatter_ex, к которому можно подключать библиотеки, исполняемы файлы и т.д.

>add_library(formatter_ex STATIC formatter_ex.cpp) создает статическую (STATIC) библиотеку (с именем formatter_ex) из указываемых файлов (formatter_ex.cpp)

>add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter) включает в сборку директорию с библиотекой formatter

>target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}) связывает библиотеку formatter_ex и CMAKE_CURRENT_SOURCE_DIR

>target_link_libraries(formatter_ex formatter) добавление библиотеки formatter

Добавляем файлы formatter_ex.cpp и formatter_ex.h в папку "formatter_ex_lib" 

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_ex_lib/formatter_ex.cpp
wget https://raw.githubusercontent.com/tp-labs/lab03/master/formatter_ex_lib/formatter_ex.h
```

Проверяем работоспособность:

```
$ cmake -H. -B_build
$ cmake --build _build
```


## III Часть

### Для hello world

Выходим из прошлой директории (возвращаемся в lab-03). Создаём в папке lab-03 директорию hello_world_application. Заходим туда:

```
$ cd ..
$ mkdir hello_world_application
$ cd hello_world_application
```

Создаём пустой файл CMakeLists.txt

```
$ cat >> CMakeLists.txt << EOF
```

Выскакивает значок " > " Записываем туда EOF. Затем редактируем этот файл:

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

>cmake_minimum_required указывает подходящую минимальную версию Cmake

>set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake
>(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)

>project(hello_world_example) создает проект hello_world_example, к которому можно подключать библиотеки, исполняемы файлы и т.д.

>add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex) включает в сборку директорию с библиотекой formatter_ex

>add_executable(example hello_world.cpp) добавляет исполняемый файл example (то, что ожидается от компиляции файла "hello_world.cpp")

>target_link_libraries(example formatter_ex) добавление библиотеки formatter_ex

Добавляем файл hello_world.cpp в папку "hello_world_application" 

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/hello_world_application/hello_world.cpp
```

Проверяем работоспособность:

```
$ cmake -H. -B_build
$ cmake --build _build
```

Запускаем сборку с целью example вместо цели по умолчанию. Выполняем сборку и выводим на экран:

```
$ cmake --build _build --target example 
$ ./_build/example
```

Выводится: hello, world!


### Для solver

Выходим из прошлой директории (возвращаемся в lab-03). Создаём в папке lab-03 директорию solver_lib. Заходим туда:

```
$ cd .. 
$ mkdir solver_lib
$ cd solver_lib 
```

Создаём пустой файл CMakeLists.txt

```
$ cat >> CMakeLists.txt << EOF
```

Выскакивает значок " > " Записываем туда EOF. Затем редактируем этот файл:

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

>cmake_minimum_required указывает подходящую минимальную версию Cmake

>set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake
>(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)

>project(solver_lib) создает проект solver_lib, к которому можно подключать библиотеки, исполняемы файлы и т.д.

>add_library(solver_lib STATIC solver.cpp) создает статическую (STATIC) библиотеку (с именем solver_lib) из указываемых файлов (solver.cpp)

>target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}) связывает библиотеку solver_lib и CMAKE_CURRENT_SOURCE_DIR

Добавляем файлы solver.cpp и solver.h в папку "solver_lib" 

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/solver_lib/solver.cpp
wget https://raw.githubusercontent.com/tp-labs/lab03/master/solver_lib/solver.h
```

При проверке на ошибки выдаёт ошибку. Меняем содержимое файла solver.cpp:

```
$ nano solver.cpp
```

Содержимое файла solver.cpp:

```
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

Снова проверяем на работоспособность:

```
$ cmake -H. -B_build
$ cmake --build _build
```


Выходим из прошлой директории (возвращаемся в lab-03). Создаём в папке lab-03 директорию solver_application. Заходим туда:

```
$ cd .. 
$ mkdir solver_application
$ cd solver_application 
```

Создаём пустой файл CMakeLists.txt

```
$ cat >> CMakeLists.txt << EOF
```

Выскакивает значок " > " Записываем туда EOF. Затем редактируем этот файл:

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

>cmake_minimum_required указывает подходящую минимальную версию Cmake

>set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake
>(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)

>project(solver_example) создает проект solver_example, к которому можно подключать библиотеки, исполняемы файлы и т.д.

>add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib ${CMAKE_CURRENT_BINARY_DIR}/solver_lib) включает в сборку директорию с библиотекой solver_lib

>add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex) включает в сборку директорию с библиотекой formatter_ex

>add_executable(example equation.cpp) добавляет исполняемый файл example (то, что ожидается от компиляции файла "equation.cpp")

>target_link_libraries(example solver_lib formatter_ex) добавление библиотеки formatter_ex

Добавляем файл equation.cpp в папку "solver_application"

```
wget https://raw.githubusercontent.com/tp-labs/lab03/master/solver_application/equation.cpp
```

Проверяем работоспособность:

```
$ cmake -H. -B_build
$ cmake --build _build
```

Запускаем сборку с целью example вместо цели по умолчанию. Выполняем сборку и выводим на экран:

```
$ cmake --build _build --target example
$ ./_build/example
```

## Скрины

I Часть

![image](https://user-images.githubusercontent.com/125077130/224117065-f65bc5bd-93fc-40c7-80ca-fb17ccd0274e.png)

![image](https://user-images.githubusercontent.com/125077130/224117113-3f508a6e-e6a9-4520-8bbd-41ae52e237f9.png)

II Часть

![image](https://user-images.githubusercontent.com/125077130/224117145-a1e1838f-1521-4d9b-b0e0-491dd56852a3.png)

![image](https://user-images.githubusercontent.com/125077130/224117163-5e35c6f9-e541-41b1-9069-249a442c157c.png)

III Часть

![image](https://user-images.githubusercontent.com/125077130/224117197-f1b94a7d-d613-44c1-9d5e-84e19c9ce7db.png)

![image](https://user-images.githubusercontent.com/125077130/224117226-eec278f2-c6cb-4fbb-b715-42599c9a6f86.png)

![image](https://user-images.githubusercontent.com/125077130/224117260-4183cc7f-bfee-448e-b2d7-774322694861.png)

![image](https://user-images.githubusercontent.com/125077130/224117302-52df123f-a2af-486c-9d32-6da30dd1508d.png)
