# HBuilder X 云打包操作指南

## 项目创建

一般都是先在HBuilder X的菜单栏创建项目才能使用HBuilder的云打包功能，所以整体流程以此为例。

1. 点击左上角菜单栏的文件板块
2. 在二级菜单栏中选择“新建”
3. 三级菜单选择“项目”
4. 选择软件提供的基础框架“uni-app”的默认模版
5. 将自己的项目迁移到软件提供的框架项目中

---

## 项目代码

如果是CSS、HTML、js文件迁移到Vue格式中，可以直接把项目源码喂给AI直接转化为Vue格式的文件。

---

## 模拟运行

在编写完代码之后就可以进行模拟调试了，可以用USB连接手机也可以在模拟器上运行

---

## 自有证书云打包

一般云打包可以选择自有证书打包，也可以选择运端证书和公共测试证书，获取自有证书也不费事，也是免费的。

1. 一级菜单选择发行
2. 二级菜单选择`App-Android/iOS-云打包`
3. 选择获取的自有证书文件（后缀为.keystore）
4. 证书库密码与证书私钥密码一致（在获取自有证书的时候自己设置的）
5. 证书别名可通过`Java`的数据证书管理工具`Keytool`获取
6. 调整广告设置
7. 最后选择底部的快速安心打包即可

---

## 创建自有证书

1. **命令行指令创建**
如果想要创建自有证书，可通过调出“命令提示符”窗口，在窗口中输入cmd，打开命令行输入如下命令

```bash
keytool -genkey -alias android.keystore -keyalg RSA -validity 36500 -keystore android.keystore
```

这句话的意思是：创建了一个名为android.keystore的别名也为android.keystore的采用RSA加密算法的有效期为100年的证书文件。
   注：
    -genkey 生成文件。
    -alias 别名。
    -keyalg 加密算法。
    -validity 有效期。
    -keystore 文件名。
2. **填写相应信息**
然后填写依次填写相关信息，最后如果确认无误的话填“y”，如果有错误的话按“Enter”，重新再填。
当输入"y"后没有回提示输入“输入<android.keystore>的密钥口令”，如果跟密钥库口令一样就按回车键，否则输入，然后再确认，就生成了数字证书。

---

## 查看证书库密码和别名

你可以使用 Java 的 `keytool` 工具来查看 keystore 文件中的信息。`keytool` 是 JDK 自带的一个工具，用于管理密钥和证书。

1. **确保已安装 JDK**：
   - 打开终端或命令提示符，运行以下命令检查是否安装了 JDK：

     ```bash
     java -version
     ```

   - 如果未安装 JDK，请从 [Oracle JDK](https://www.oracle.com/java/technologies/javase-downloads.html) 或 [OpenJDK](https://openjdk.org/) 下载并安装。

2. **使用 `keytool` 查看证书信息**：
   - 运行以下命令查看 keystore 文件中的信息：

     ```bash
     keytool -list -v -keystore your_keystore_file.jks
     ```

     - 将 `your_keystore_file.jks` 替换为你的 keystore 文件路径。
   - 系统会提示你输入 **keystore 密码**。如果密码正确，会显示 keystore 中的所有证书信息，包括 **别名（Alias）**。

---
