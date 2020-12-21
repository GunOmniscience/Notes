# winform

## 1.怎么修改窗体标题

​	设计     Text

## 2.怎么修改窗体左上角图标

图标默认大小32*32px

窗口样式    Icon

## 3.怎么设置窗体出现位置

​	布局     StartPosition



## 4.怎么固定窗体大小

   布局   AutoSizeMode

5.MessageBox参数

MessageBox.show("提示内容信息", "提示标题", MessageBoxButtons.OKCancel, MessageBoxIcon.Question)

返回值与 DialogResult.Cencel 判断

## 6.阻止窗体关闭

在窗体的FormClosing事件中将事件参数e.Cancel设置成true

## 7.正则表达式

导包：using System.Text.RegularExpressions

new Regex("^\\d+$")

调用Regex的实例函数：isMatch()函数      返回bool

## 8.MDI子窗体

在这个窗体show之前设置！！！！！！！
this.parentMDI这个别忘了设置

## 9.别忘了写注释

## 10.别忘了命名规范

## 11.Combobox

获取SelectId当id时记得他是从0开始的所以得+1

插入“请选择”cbm.Items.Insert(下标，"");

## 12.ListView

ListViewItem row = new ListViewItem(data[0].ToString());
                row.SubItems.Add(data[1].ToString());
                row.SubItems.Add(data[2].ToString());
                row.SubItems.Add(data[3].ToString());
                row.SubItems.Add(data[4].ToString());
                row.SubItems.Add(data[5].ToString());
                lvInfo.Items.Add(row);

## 13.比较日期

like用于专门进行字符串匹配 类似于正则表达式
= 用于专门进行值的比较例如日期等等