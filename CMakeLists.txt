file(GLOB SRCS
     src/*.cpp
     src/utils/aw9523/*.cpp
     src/utils/ina226/*.cpp
     src/utils/lm75b/*.cpp
     src/utils/modbus_params/*.c
     src/utils/pi4ioe5v6408/*.cpp
     src/utils/rx8130/*.cpp)

if(ARDUINO_ARCH_ESP32)
     list(APPEND COMPONENT_REQUIRES M5Unified arduino)
elseif(IDF_VERSION_MAJOR LESS 5)
     list(APPEND COMPONENT_REQUIRES M5Unified freemodbus)
else()
     list(APPEND COMPONENT_REQUIRES M5Unified)
endif()

idf_component_register(SRCS ${SRCS}
                       INCLUDE_DIRS "src" "src/utils"
                       REQUIRED_IDF_TARGETS esp32s3
                       REQUIRES ${COMPONENT_REQUIRES})
