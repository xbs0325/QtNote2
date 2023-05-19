# QtNote2
Qt笔记02
# 资源文件

1.图片拷贝到根目录下

2.右键项目->添加新文件->Qt Resource File->创建.qrc文件->open in editor打开编辑

->添加前缀->添加文件
->setIcon(QIcon(":前缀名/文件名称"))

# 模态非模态对话框创建

## 模态创建

`QDialog dlg(this);`

阻塞程序

`dlg.exec()`

## 非模态创建

为防止一闪而过(在匿名函数中 运行完便会被释放)
```
QDialog * dlg2 = new QDialog(this);
dlg2->show();
```
设置自动释放空间

`dlg2->setAtrribute(Qt::WA_DeleteOnClose)`

# 标准对话框

## 消息对话框
QMessage窗口
```
QMessageBox::information(QWidget *parent, const QString &title, const QString &text, QMessageBox::StandardButtons buttons = Ok QMessageBox::StandardButton defaultButton = NoButton)

QMessageBox::warning(QWidget *parent, const QString &title, const QString &text, QMessageBox::StandardButtons buttons = Ok QMessageBox::StandardButton defaultButton = NoButton)

QMessageBox::critical(QWidget *parent, const QString &title, const QString &text, QMessageBox::StandardButtons buttons = Ok QMessageBox::StandardButton defaultButton = NoButton)

QMessageBox::question(QWidget *parent, const QString &title, const QString &text, QMessageBox::StandardButtons buttons = StandardButtons(Yes | No)
QMessageBox::StandardButton defaultButton = NoButton)
```
第一个参数parent 第二个参数标题文本 第三个参数主要内容 第四个参数按钮 第五个默认关联按钮

例如:
`QMessageBox::question(this,"question","是否保存",QMessageBox::Save|QMessageBox::Cancel,QMessageBox::Cancel);`

如何捕捉用户选项？
->返回值为QMessageBox::StandardButton类型
对返回值进行判断

# 其他标准对话框
## 颜色对话框
例:

`QColor coler1 = QColorDialog::getColor(QColor(255,0,0));`

等价于

```
QColorDialog dialog;
dialog.setCurrentColor(coler1);
```
  
其中`QColor(int r, int g, int b, int a = 255)`

r->red g->green b->blue a->透明度

## 文件对话框
例:
```
QString fileName = QFileDialog::getOpenFileName(this,"打开.txt文件","C:/Users/as/Desktop","*.txt");
qDebug() << fileName;
```
## 字体对话框
例:
```
bool flag;
QFont font = QFontDialog::getFont(&flag,QFont("华文彩云",36));
qDebug() << "字体: "<< font.family().toUtf8().data()<<" 字号: "<<font.pointSize() <<" 是否加粗: "<<font.bold()<<" 是否倾斜: "<<font.italic();
```

