## Instructions

My name is He Longzhu, from Dezhou city, Shandong Province. I am studying in The Computer School of Beijing University of Posts and Telecommunications, majoring in software engineering. This is one of my test pages.


### My Work

Here is my Python code for this machine-built experiment.

```markdown
from pynput.keyboard import Key, Listener
from direction import Direction
import os


class Control():

    def __init__(self):
        self.dir_ = None  # dir一定要用成员变量，不然没办法在on_press中修改
        self.x1 = float(0)
        self.x2 = float(0)
        self.x3 = float(0)
        self.x4 = float(0)
        self.x5 = float(0)

    def getdir(self):

        self.dir_ = None  # 如果是不是上下左右则返回None

        def on_press(key):

            if key == Key.up:
                self.dir_ = Direction.UP
                x1 = self.x1 + 0.1
                os.system("rostopic pub -1 /mrm/joint1_position_controller/  \
                                command std_msgs/Float64 \"data: {y1}\"".format(y1=x1))
            elif key == Key.down:
                self.dir_ = Direction.DOWN
                x2 = self.x2 - 0.1
                os.system("rostopic pub -1 /mrm/joint2_position_controller/  \
                               command std_msgs/Float64 \"data: {y2}\"".format(y2=x2))
            elif key == Key.left:
                self.dir_ = Direction.LEFT
                x3 = self.x3 + 0.1
                os.system("rostopic pub -1 /mrm/joint3_position_controller/  \
                                               command std_msgs/Float64 \"data: {y3}\"".format(y3=x3))
            elif key == Key.right:
                self.dir_ = Direction.RIGHT
                x4 = self.x4 - 0.1
                os.system("rostopic pub -1 /mrm/joint4_position_controller/  \
                                                               command std_msgs/Float64 \"data: {y4}\"".format(y4=x4))
            return False

        listener = Listener(on_press=on_press)  # 创建监听器
        listener.start()  # 开始监听，每次获取一个键
        listener.join()  # 加入线程
        listener.stop()  # 结束监听，没有这句也行，直接随函数终止
        return self.dir_


if __name__ == '__main__':
    c = Control()
    i = 0
    while True:
        i += 1
        print(i, c.getdir())
```



### END

I will continue to improve this page in the future.
