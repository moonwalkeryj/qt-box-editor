cmake_minimum_required(VERSION 2.8 FATAL_ERROR) 

project(QtBoxEditor)
set(EXE_NAME QtBoxEditor)
set(PROJECT_NAME QtBoxEditor)

#Pacages for Tesseract
set(TESSERACT_DIR
        "C:/Program Files/Tesseract-OCR"
)

include_directories(${TESSERACT_DIR}/include)

set(TESS_LIBS
	${TESSERACT_DIR}/lib/libtesseract302.lib
	${TESSERACT_DIR}/lib/liblept168.lib
)

list(APPEND ADDITIONAL_LIBS ${TESS_LIBS})
message(${ADDITIONAL_LIBS})

#Pacages for Qt
find_package(Qt4 REQUIRED)
find_package(Qt4 COMPONENTS QtCore QtGui QtNetwork QtXml REQUIRED)
include(${QT_USE_FILE})
list(APPEND ADDITIONAL_LIBS ${QT_LIBRARIES})

#HEADER NON-QOBJECT
set(INCS
				src/Settings.h 
				src/TessTools.h
)

set(SRCS
)

#FORMS
set(UI_SHORT_CUT_DIALOG 		dialogs/ShortCutDialog.ui)
set(UI_GET_ROW_ID_DIALOG    	dialogs/GetRowIDDialog.ui)
set(UI_SETTINGS_DIALOG			dialogs/SettingsDialog.ui)
set(UI_FIND_DIALOG				dialogs/FindDialog.ui)
set(UI_DRAW_RECTANGLE			dialogs/DrawRectangle.ui)

QT4_WRAP_UI(UI_SHORT_CUT_DIALOG_INC     ${UI_SHORT_CUT_DIALOG})
QT4_WRAP_UI(UI_SHORT_CUT_DIALOG_INC 	${UI_SHORT_CUT_DIALOG})
QT4_WRAP_UI(UI_GET_ROW_ID_DIALOG_INC	${UI_GET_ROW_ID_DIALOG})
QT4_WRAP_UI(UI_SETTINGS_DIALOG_INC		${UI_SETTINGS_DIALOG})
QT4_WRAP_UI(UI_FIND_DIALOG_INC			${UI_FIND_DIALOG})
QT4_WRAP_UI(UI_DRAW_RECTANGLE_INC		${UI_DRAW_RECTANGLE})

list(APPEND INCS ${UI_SHORT_CUT_DIALOG_INC} 
                 ${UI_SHORT_CUT_DIALOG_INC}
                 ${UI_GET_ROW_ID_DIALOG_INC}
                 ${UI_SETTINGS_DIALOG_INC}
                 ${UI_FIND_DIALOG_INC}
                 ${UI_DRAW_RECTANGLE_INC}
)

#CPP SOURCES
set(SRCS
    src/main.cpp
    src/MainWindow.cpp 
    src/ChildWidget.cpp 
    src/DelegateEditors.cpp 
    src/TessTools.cpp 
    dialogs/SettingsDialog.cpp 
    dialogs/GetRowIDDialog.cpp 
    dialogs/ShortCutsDialog.cpp 
    dialogs/FindDialog.cpp 
    dialogs/DrawRectangle.cpp
)

#HEADER QOBJECT
set(MOC_MAIN_WINDOW_INC		src/MainWindow.h)
set(MOC_CHILD_WIDGET_INC    	src/ChildWidget.h) 
set(MOC_DELEGATE_EDITORS_INC    src/DelegateEditors.h)
set(MOC_SETTINGS_DIALOG_INC    	dialogs/SettingsDialog.h)
set(MOC_GET_ROW_ID_DIALOG_INC   dialogs/GetRowIDDialog.h)
set(MOC_SHORT_CUTS_DIALOG_INC   dialogs/ShortCutsDialog.h)
set(MOC_FIND_DIALOG_INC    	dialogs/FindDialog.h)
set(MOC_DRAW_RECTANGLE_INC	dialogs/DrawRectangle.h)

QT4_WRAP_CPP(MOC_MAIN_WINDOW_SRC	${MOC_MAIN_WINDOW_INC})
QT4_WRAP_CPP(MOC_CHILD_WIDGET_SRC    	${MOC_CHILD_WIDGET_INC})
QT4_WRAP_CPP(MOC_DELEGATE_EDITORS_SRC   ${MOC_DELEGATE_EDITORS_INC})
QT4_WRAP_CPP(MOC_SETTINGS_DIALOG_SRC   	${MOC_SETTINGS_DIALOG_INC})
QT4_WRAP_CPP(MOC_GET_ROW_ID_DIALOG_SRC  ${MOC_GET_ROW_ID_DIALOG_INC})
QT4_WRAP_CPP(MOC_SHORT_CUTS_DIALOG_SRC  ${MOC_SHORT_CUTS_DIALOG_INC})
QT4_WRAP_CPP(MOC_FIND_DIALOG_SRC    	${MOC_FIND_DIALOG_INC})
QT4_WRAP_CPP(MOC_DRAW_RECTANGLE_SRC	${MOC_DRAW_RECTANGLE_INC})

list(APPEND INCS ${MOC_MAIN_WINDOW_INC}
                 ${MOC_CHILD_WIDGET_INC}
                 ${MOC_DELEGATE_EDITORS_INC}
                 ${MOC_SETTINGS_DIALOG_INC}
                 ${MOC_GET_ROW_ID_DIALOG_INC}
                 ${MOC_SHORT_CUTS_DIALOG_INC}
                 ${MOC_FIND_DIALOG_INC}
                 ${MOC_DRAW_RECTANGLE_INC}
				 )
list(APPEND SRCS ${MOC_MAIN_WINDOW_SRC}	
                 ${MOC_CHILD_WIDGET_SRC}
                 ${MOC_DELEGATE_EDITORS_SRC}
                 ${MOC_SETTINGS_DIALOG_SRC}
                 ${MOC_GET_ROW_ID_DIALOG_SRC}
                 ${MOC_SHORT_CUTS_DIALOG_SRC}
                 ${MOC_FIND_DIALOG_SRC}
                 ${MOC_DRAW_RECTANGLE_SRC}
				 )

#QT RESOURCES
SET(APPLICATION_RESOURCES 	resources/application.qrc)
SET(QBE_GNOME_RESOURCES 	resources/QBE-GNOME.qrc)
SET(QBE_FAENZA_RESOURCES 	resources/QBE-Faenza.qrc)
SET(QBE_OXYGEN_RESOURCES 	resources/QBE-Oxygen.qrc)
SET(QBE_TANGO_RESOURCES 	resources/QBE-Tango.qrc)

QT4_ADD_RESOURCES(APPLICATION_RESOURCES_RCC	${APPLICATION_RESOURCES})
QT4_ADD_RESOURCES(QBE_GNOME_RESOURCES_RCC	${QBE_GNOME_RESOURCES})
QT4_ADD_RESOURCES(QBE_FAENZA_RESOURCES_RCC	${QBE_FAENZA_RESOURCES})
QT4_ADD_RESOURCES(QBE_OXYGEN_RESOURCES_RCC	${QBE_OXYGEN_RESOURCES})
QT4_ADD_RESOURCES(QBE_TANGO_RESOURCES_RCC	${QBE_TANGO_RESOURCES})

set(RCCS
)

list(APPEND RCCS ${APPLICATION_RESOURCES_RCC}
                 ${QBE_GNOME_RESOURCES_RCC}
                 ${QBE_FAENZA_RESOURCES_RCC}
                 ${QBE_OXYGEN_RESOURCES_RCC}
                 ${QBE_TANGO_RESOURCES_RCC}
)

### include current dir
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})

#### build
add_executable(${EXE_NAME} ${SRCS} ${INCS} ${RCCS})
target_link_libraries(${EXE_NAME} ${ADDITIONAL_LIBS})
