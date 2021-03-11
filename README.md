### Представьте, что вы стажер в компании "Formatter Inc.".
Part 1
### Вам поручили перейти на систему автоматизированной сборки CMake. Исходные файлы находятся в директории formatter_lib. В этой директории находятся файлы для статической библиотеки formatter. Создайте CMakeList.txt в директории formatter_lib, с помощью которого можно будет собирать статическую библиотеку formatter.
1) Чтобы настрить систему автоматической сборки, необходимо создать CMakeLists.txt
2) В созданном файле я прописал следующие команды:
> cmake_minimum_required(VERSION 3.4)
> add_library(formatter STATIC formatter.h formatter.cpp)
2) Чтобы система заработала, нам необходимо указать cmake адрес нашего файла, что мы делаем с помощью команды $cmake ~/Berendei-Jr/workspace/projects/lab03/formatter_lib/
3) Далеее я запустил автоматическую сборку командой $make, чтобы получить файл библиотеки

Part 2
### У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием CMakeList.txt для статической библиотеки formatter, ваш руководитель поручает заняться созданием CMakeList.txt для библиотеки formatter_ex, которая в свою очередь использует библиотеку formatter.
1) Данный проект требует подключения библиотеки, поэтому мне необходимо внести следующие изменения в СMakeLists.txt
> cmake_minimum_required(VERSION 3.4)
> project(formatter_ex)
> include_directories(formatter_lib)
> add_subdirectory(formatter_lib)
> add_library(formatter_ex STATIC formatter_ex.h formatter_ex.cpp)
> target_link_libraries(formatter_ex formatter)
2) Затем мы переносим библиотеку formatter_lib в репозиторий
3) Далее приступаем к сборке проекта.

Part 3
### Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой formatter_ex, вам необходимо создать два CMakeList.txt для двух простых приложений:

###    hello_world, которое использует библиотеку formatter_ex;
###    solver, приложение которое испольует статические библиотеки formatter_ex и solver_lib.

### Удачной стажировки!

1) В папке каждого приложения создаем СMakeLists.txt. hello_world: 
> cmake_minimum_required(VERSION 3.4)
> project(hello_world)
> include_directories(formatter_ex_lib)
> add_subdirectory(formatter_ex_lib)
> add_executable(hello_world hello_world.cpp)
> target_link_libraries(hello_world formatter_ex)

solver:

> cmake_minimum_required(VERSION 3.4)
> project(solver)
> add_executable(solver equation.cpp)
> include_directories(formatter_ex_lib)
> add_subdirectory(formatter_ex_lib)
> include_directories(solver_lib)
> add_subdirectory(solver_lib)
> target_link_libraries(solver formatter_ex)
> target_link_libraries(solver solver_lib)

2) Настраиваем систему автоматической сборки в библиотеке Solver:

> cmake_minimum_required(VERSION 3.4)
> add_library(solver_lib STATIC solver.h solver.cpp)

3) Собираем проект, но получаем ошибку.
4) Чтобы решить проблему, в исходный файл библиотеки Solver_lib необходимо подключить библиотеку math.h
5) Запускаем оба приложения: hello_world:
> world 
> -------------------------
> hello, world!
> -------------------------

solver:

> 1
> 4
> 4
> -------------------------
> x1 = -2.000000
> -------------------------
> -------------------------
> x2 = -2.000000
> -------------------------
