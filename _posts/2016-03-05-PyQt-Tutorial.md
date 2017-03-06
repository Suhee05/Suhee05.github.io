---
layout: post
title: PyQt Tutorial
---

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

- Saving the result in .py

1. Convert .ui file to .py file using pyuic5 command

```
cd /Applications/anaconda/bin 
```
Go to Terminal. Find the folder where pyuic5 is.

```
pyuic5 -x YOUR UIFILE PATH -o OUTPUT FILE PATH

//pyuic5 -x /Users/josuhee/Documents/PythonGUI/test.ui -o /Users/josuhee/Documents/PythonGUI/test.py  
```
pyuic5 command is executed. Be sure to check your current version. For Qt 4, the command is pyuic4.


```
exec python -m PyQt5.uic.pyuic youruifile -o yourpyfile -x
```
If any error occurs, google the error. In my case, "module not found" was on the error message. The line above helped me a lot.



 



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


- QLabel

- QlineEdit

- QPushButton

- QRadioButton

- QCheckBox

- QComboBox

- QSpinBox

- QSlider Widget & Signal

- QMenuBar, QMenu & QAction

- QToolBar

- QInputDialog

- QFontDialog

- QFileDialog

- QTab

- QStacked

- QSplitter

- QDock

- QStatusBar

- QList

- QScrollBar

- QCalendar



## Layout

- setGeometry()

```
QWidget.setGeometry(xpos, ypos, width, height)
```
## Signals and Slots

- Event

User's actions. For example, a button click, selecting an item.

- Signal

In response to one or more events, PyQt widgets send signal.
Signal does not induce any action.

- Slot

The signal is connected to Slot, which is a Python callable function.
One signal can be connected to many slots. 

For more info, http://pyqt.sourceforge.net/Docs/PyQt4/new_style_signals_slots.html

## Example

### Basic Frame

```
#1st example

import sys
from PyQt5 import QtCore, QtGui, QtWidgets # Import modules from PyQt5

class Ui_MainWindow(QMainWindow): #Class for your GUI. In this case, Ui_MainWindow inherited class from QMainWindow.
    def __init__(self): #Initiation of Ui_MainWindow
        super().__init__() #Initiation of QMainWindow
        self.setupUi() #Set up layout & signals and slots
        
    def setupUi(self):
        self.setGeometry(500, 500, 800, 600)
        
        title_label = QtWidgets.QLabel("Cm to Inch", self)
        title_label.move(310, 60)
        title_label.resize(201, 51)
        font = QtGui.QFont()
        font.setPointSize(40)
        title_label.setFont(font)
        title_label.setAlignment(QtCore.Qt.AlignCenter)
        
        cm_label = QtWidgets.QLabel("Cm", self)
        cm_label.move(190, 120) #Since there is QtCore, cm_label.setGeometry(QtCore.QRect(520, 120, 91, 41))
        cm_label.resize(91, 41)
        font = QtGui.QFont()
        font.setPointSize(19)
        cm_label.setFont(font)
        cm_label.setAlignment(QtCore.Qt.AlignCenter)
        
        inch_label = QtWidgets.QLabel("Inch", self)
        inch_label.move(520, 120)
        inch_label.resize(91, 41)
        font = QtGui.QFont()
        font.setPointSize(19)
        inch_label.setFont(font)
        inch_label.setAlignment(QtCore.Qt.AlignCenter)
        
        
        self.input_lineEdit = QtWidgets.QLineEdit("",self)
        self.input_lineEdit.move(160, 180)
        self.input_lineEdit.resize(160, 80)
        
        self.result_label = QtWidgets.QLabel("", self) # Other function (not setupUi) refers this label. 
        self.result_label.move(490, 180)
        self.result_label.resize(160, 80)
        font = QtGui.QFont()
        font.setPointSize(33)
        self.result_label.setFont(font)
        
        
        convert_button = QtWidgets.QPushButton("Convert",self)
        convert_button.move(350,350)
        convert_button.resize(113,32)
        convert_button.clicked.connect(self.btn_clicked)
		
	def btn_clicked(self):
		 cm_input = float(self.input_lineEdit.text())
		 inch_output = cm_input * 0.393701
		 self.result_label.setText(str(inch_output))
   
if __name__ == "__main__": # These lines below are essential for running 
    app = QApplication(sys.argv)
    mywindow = Ui_MainWindow()
    mywindow.show()
    app.exec_() 
        

```



- ! contains Quotes from the official page (Classes)


