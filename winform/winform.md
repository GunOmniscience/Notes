# WinForm

## 1.BackgroundImage

-  BackgroundImageLayout 背景图片自适应

  true，false




## 2.winform文件

- .cs 窗体文件，我们的代码往这里写

- .Designer.cs 窗体设计文件：VS自动生成的，我们不修改它

- .resx 资源文件，用来配置当前窗体所使用的字符串、图片资源等

- Program.cs 主程序文件，其中包含main方法

  “Application.Run(new 窗体类名());” 的含义是应用程序启动时运行的窗体

## 3.主窗体

**属性：**

|      属性       |                             说明                             |
| :-------------: | :----------------------------------------------------------: |
|   MaximizeBox   |                      窗体是否可以最大化                      |
|   WindowState   | 窗体的初始状态：noraml普通,maximized最大化，minimized最小化，默认为normal |
| FormBorderStyle |           FixedSingle用户无法通过拖拽调整窗口大小            |

**方法：**

|     方法     |      说明      |
| :----------: | :------------: |
|   Close()    |    关闭窗体    |
|    Show()    |    显示窗体    |
| ShowDialog() | 模式化显示窗口 |
|    Hide()    |    隐藏窗体    |

## 4.Label

内容无法被用户更高

**属性：**

| 属性  |        说明        |
| :---: | :----------------: |
| Image |  在标签上显示图像  |
| Text  | 在标签上显示的文本 |

## 5.TextBox

**属性：**

|     属性     |                          说明                          |
| :----------: | :----------------------------------------------------: |
|  MaxLength   |           指定可以在文本框中输入的最大字符数           |
|  Multiline   |             是否可以在文本框中输入多行文本             |
| PassWordChar | 作为密码框时，文本框中显示的字符，而不是实际输入的文本 |

## 6.ComboBox

允许用户在框中输入或选择下拉列表项

**属性：**

|     属性      |                      说明                      |
| :-----------: | :--------------------------------------------: |
|     Items     |                  组合框中的项                  |
| DropDownStyle | 是否显示列表框部分，是否允许用户编辑文本框部分 |
| SelectedIndex |       当前选定项目的索引号，下标从0开始        |
| SelectedItem  |                获取当前选定的项                |

**事件：**

|         事件         |             说明              |
| :------------------: | :---------------------------: |
|        Click         |          单击控件时           |
| SelectedIndexChanged | 在SelectedIndex属性修改后发生 |

## 7.Button

**属性：**

|   属性    |         说明         |
| :-------: | :------------------: |
| TextAlign | 按钮上文本的对齐方式 |

## 8.命名规范

控件类名的缩写+有含义的英文单词

## 9.添加控件到窗口上

this.Controls.Add() this代表当前的窗体对象，将控件对象添加到窗体的控件集合中，这样控件就能在窗体上显示出来

**案例：**

```c#
this.Controls.Add(this.cboLoginType);
```

## 10.事件函数

**事件函数代码：**

```C#
private void btnCancel_Click(object sender, EventArgs e)
{
    this.Close();
}
```

- sender 事件源，发生了这个事件的对象，我们可以通过sender得到发生事件的控件，这需要进行强制类型转换
- e 事件参数对象

## 11.MessageBox消息框

**标准代码：**

```C#
MessageBox.Show("要显示的字符串","消息框的标题",消息框的按钮,消息框的图标);
```

**案例：**

```c#
MessageBox.Show("确认取消登录吗？","操作提示",MessageBoxButtons.YesNo,Message.Question);
```

## 12.窗体间的跳转

1. 创建我们即将显示的窗口的实例对象
2. 调用这个对象的Show()
3. this.Hide()将我们当前窗口隐藏

