cmake_minimum_required(VERSION 3.10)
project(mainwindow LANGUAGES CXX)

# dosya ismi
PROJECT ( mainwindow )


# Enable C++11
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_AUTOMOC TRUE)

# https://stackoverflow.com/questions/34143265/undefined-reference-to-symbol-pthread-createglibc-2-2-5
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")

# Define project name
project(opencv_example_project)

find_package(OpenCV REQUIRED)

#find_package(Qt5 COMPONENTS REQUIRED Quick Qml Core Gui Widgets)
find_package(Qt5 COMPONENTS Core Gui Widgets REQUIRED)


include_directories(
    ${OpenCV_INCLUDE_DIRS}
)

link_directories(
    ${OpenCV_LIB_DIR}
)

# Declare the executable target built from your sources

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(project_sources 
./mainwindow.cpp 
./main.cpp
./ip_url.cpp
)

set(project_headers 
./mainwindow.h
./ip_url.h
)

set(project_ui 
  ./ip_url.ui
  ./mainwindow.ui)

# wrap the ui file to a c++ header
qt5_wrap_ui(ui_wrap ${project_ui})
qt5_wrap_cpp(moc_sources ${project_headers})
add_executable(opencv_example_project 
	${project_sources} 
	${project_headers}
	${ui_wrap} 
	${moc_sources})
target_link_libraries(opencv_example_project 
	PUBLIC
	Qt5::Core
	Qt5::Gui 
	Qt5::Widgets
  ${OpenCV_LIBS})

# need this to include the auto generated ui_mainwindow.h 
# file from the qt5_wrap_ui call below.
set(CMAKE_INCLUDE_CURRENT_DIR ON)
