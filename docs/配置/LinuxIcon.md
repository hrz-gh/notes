# Linux 日常

## 应用图标

桌面快捷方式存放位置：`/usr/share/applications/`

Format:

```icon
#文件头
[Desktop Entry]

#编码方式
Encoding=UTF-8  

#应用程序名称，根据当前系统语言匹配显示，优先匹配更细化的语言标识名称
Name=aMule  
Name[en]=en_name
Name[en_US]=US_name 

#鼠标经过上面时的提示名称，也可国际化
Comment=comment  

#菜单执行的命令或程序
Exec=command  

#显示在菜单项中的图标，可以为空
Icon=iconpath  

#是否使用终端
Terminal=false  

#分类
Type=Application 

#菜单是否隐藏，类似NoDisplay属性
Hidden=false

#菜单所属类别，可以确定该菜单的位置
Categories=Application;Network;
```

## vim 技巧

输出`vim`中内容到系统文件中:

`:w !sudo tee PATH

