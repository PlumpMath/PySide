project(QtDeclarative)

set(QtDeclarative_SRC
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativecomponent_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativecontext_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeengine_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeerror_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeexpression_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeextensionplugin_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeimageprovider_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeitem_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativelistreference_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativenetworkaccessmanagerfactory_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeparserstatus_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativepropertymap_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativepropertyvaluesource_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeproperty_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativescriptstring_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qdeclarativeview_wrapper.cpp
${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/qtdeclarative_module_wrapper.cpp
)

execute_generator(declarative QtDeclarative_SRC "${CMAKE_CURRENT_BINARY_DIR}:${QtCore_SOURCE_DIR}:${QtGui_BINARY_DIR}:${QtGui_SOURCE_DIR}:${QtDeclarative_SOURCE_DIR}:${QtNetwork_SOURCE_DIR}:${QtNetwork_BINARY_DIR}")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}
                    ${QT_QTCORE_INCLUDE_DIR}
                    ${QT_QTGUI_INCLUDE_DIR}
                    ${QT_QTNETWORK_INCLUDE_DIR}
                    ${QT_QTDECLARATIVE_INCLUDE_DIR}
                    ${PYTHON_INCLUDE_PATH}
                    ${SHIBOKEN_INCLUDE_DIR}
                    ${libpyside_SOURCE_DIR}
                    ${QtGui_BINARY_DIR}/PySide/QtGui/
                    ${QtCore_BINARY_DIR}/PySide/QtCore/
                    ${QtNetwork_BINARY_DIR}/PySide/QtNetwork/
                    ${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative)
add_library(QtDeclarative MODULE ${QtDeclarative_SRC})
set_target_properties(QtDeclarative PROPERTIES PREFIX "")
target_link_libraries(QtDeclarative
                      pyside
                      ${PYTHON_LIBRARIES}
                      ${QT_QTCORE_LIBRARY}
                      ${QT_QTGUI_LIBRARY}
                      ${QT_QTNETWORK_LIBRARY}
                      ${QT_QTSCRIPT_LIBRARY}
                      ${QT_QTSVG_LIBRARY}
                      ${QT_QTSQL_LIBRARY}
                      ${QT_QTXMLPATTERNS_LIBRARY}
                      ${QT_QTOPENGL_LIBRARY}
                      ${QT_QTDECLARATIVE_LIBRARY})
add_dependencies(QtDeclarative QtGui)
add_dependencies(QtDeclarative QtNetwork)

# install
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/QtDeclarative${CMAKE_DEBUG_POSTFIX}.so
        DESTINATION ${SITE_PACKAGE}/PySide)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/PySide/QtDeclarative/pyside_qtdeclarative_python.h
        DESTINATION include/PySide/QtDeclarative/)
