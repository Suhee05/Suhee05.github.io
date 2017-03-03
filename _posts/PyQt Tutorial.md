# PyQt?

>PyQt is a set of Python v2 and v3 bindings for The Qt Company's Qt application framework and runs on all platforms supported by Qt including Windows, OS X, Linux, iOS and Android. 
>
> \- Riverbank Computing
> 

- Originally, Qt was a cross platform GUI Framework for C++, but Riverbank Computing created Qt for Python. This is called PyQt

- PyQt Designer comes along with PyQt. PyQt Designer is an editing tool for GUI.


# Installing on Max OS

- Download installer packages from the official site http://www.riverbankcomputing.com/

- Anaconda has PyQt inside its package. Install Anaconda and you'll see the programs like Qt Designer, Qt linguist...etc.


# Using Qt Designer

- Qt Designer starts with a window that asks for a template. Choose one and Create.


# Writing Codes

## Steps

1. Import PyQt module

2. Create Application Object

3. Set a window and widgets


## Classes

- **QObject**: The base class for all Qt Objects.(top in the hierarchy) with **QPaintDevice** which is the base class for all Qt objects that can be painted.

- **QApplication**: manages the GUI's control flow and main settings. This has the main event loop where all events are processed.

- **QWidget**: The base class for all user interface objects. This class comes from QObject and QPaintDevice

- For more info, http://pyqt.sourceforge.net/Docs/PyQt4/classes.html



### Widgets

QLabel

QlineEdit

QPushButton

QRadioButton

QCheckBox

QComboBox

QSpinBox

QSlider Widget & Signal

QMenuBar, QMenu & QAction

QToolBar

QInputDialog

QFontDialog

QFileDialog

QTab

QStacked

QSplitter

QDock

QStatusBar

QList

QScrollBar

QCalendar



## Layout

- setGeometry()

## Signals and Slots




- ! contains Quotes from the official page (Classes)


