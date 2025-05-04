cmake_minimum_required(VERSION 3.10)
project(Prk7)

# Установка стандарта C11 и включение всех предупреждений
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Wpedantic")

# Основной исполняемый файл
add_executable(prk7 src/prk7.c)

# Установка правильных прав доступа для Linux
install(TARGETS prk7
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE)

# Установка для Astra Linux (специфичные настройки)
if(EXISTS "/etc/astra_version")
    message(STATUS "Настройка для Astra Linux")
    # Дополнительные флаги для совместимости
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D_GNU_SOURCE")
endif()
