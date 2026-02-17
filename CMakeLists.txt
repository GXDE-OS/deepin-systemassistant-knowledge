cmake_minimum_required(VERSION 3.10)
project(deepin-systemassistant-knowledge)

set(CMAKE_INSTALL_PREFIX /usr/share/deepin-systemassistant-knowledge)

if (NOT DEFINED BUILD_OS_TYPE OR BUILD_OS_TYPE STREQUAL "")
    set(BUILD_OS_TYPE "")
else()
    message("catch BUILD_OS_TYPE ${BUILD_OS_TYPE}")
endif()

if (${BUILD_OS_TYPE} MATCHES "COMMUNITY")
    install(FILES deepin-knowledge/SystemAssistant.db deepin-knowledge/SystemAssistant.faiss
        DESTINATION ${CMAKE_INSTALL_PREFIX}/deepin-knowledge)
else()
    install(FILES uos-knowledge/SystemAssistant.db uos-knowledge/SystemAssistant.faiss
        DESTINATION ${CMAKE_INSTALL_PREFIX}/deepin-knowledge)

    file(GLOB knowledge_files "uos-knowledge/source/*.docx")
    install(FILES ${knowledge_files} DESTINATION ${CMAKE_INSTALL_PREFIX}/deepin-knowledge/source)
endif()