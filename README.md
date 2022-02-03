# pyqt-translucent-full-loading-screen-thread
PyQt thread which overlays the translucent loading screen with label on the whole window like some generic application loading screen.

## Requirements
PyQt5 >= 5.8

## Setup
```pip3 install git+https://github.com/yjg30737/pyqt-translucent-full-loading-screen-thread.git --upgrade```

## Example
### Code Sample
```python
import time
from PyQt5.QtWidgets import QPushButton, QTextEdit, QVBoxLayout, QWidget, QApplication

from pyqt_translucent_full_loading_screen_thread import LoadingThread

# for second example
class MyThread(LoadingThread):

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)

    def run(self):
        time.sleep(1)


class Main(QWidget):
    def __init__(self):
        super().__init__()
        self.__initUi()

    def __initUi(self):
        btn = QPushButton('Start Loading Thread')
        btn.clicked.connect(self.__startLoadingThread)
        self.__te = QTextEdit()

        lay = QVBoxLayout()
        lay.addWidget(btn)
        lay.addWidget(self.__te)

        self.setLayout(lay)

    def __startLoadingThread(self):
        self.__thread = LoadingThread(parent=self)
        # for second example
        # self.__thread = MyThread(parent=self) 
        self.__thread.start()


if __name__ == '__main__':
    import sys

    app = QApplication(sys.argv)
    window = Main()
    window.show()
    app.exec()
```

### Result of ```LoadingThread``` which is module itself

https://user-images.githubusercontent.com/55078043/152280930-ee1c8f9f-aca7-493c-aaeb-a6ec24daa75e.mp4

Loading screen is shown for 5 seconds.

### Result of ```MyThread``` which inherits the ```LoadingThread```

https://user-images.githubusercontent.com/55078043/152280946-65a9df9f-ca6e-4b01-8c43-e68304c74a66.mp4

Loading screen is shown for 1 second. Because ```run()``` method of ```MyThread``` overrides ```LoadingThread```'s.




