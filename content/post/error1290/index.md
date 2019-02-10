+++
title = "Get Rid of MySQL Error 1290 in Mac"
subtitle = ""

date = 2019-01-31T00:00:00
lastmod = 2019-01-31T00:00:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Qixing Li"]

tags = ["Data Science", "MySQL"]
summary = "Many people who use MySQL 8.0 might encounter the 1290 issue. I have done some research online and the method discussed in this post may help you to solve the problem."

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  # caption = "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""

  # Show image only in page previews?
  preview_only = true

+++

Many people who use MySQL 8.0 might encounter the 1290 issue. I have done some research online and the method discussed in this post may help you to solve the problem.

1. copy the code below to terminal and input the password to open MySQL:
```
/usr/local/mysql/bin/mysql -uroot -p
```
  + On the right top conner click the serach icon and type terminal, in case you don't know how to open a terminal.
  + password is the one you login in MySQL, usually set up when you install it. 
  
2. Copy the code below to check the directory:
```
SELECT @@GLOBAL.secure_file_priv;
```

3. if there is a `null` or `/` , open the file below:
```
/Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist
```
![](https://qixing810.github.io/content/post/error1290/gallery/1.jpg)
 + open finder, then click command+shift+G together,paste the path. 
 + use an editor to open this file: 'com.oracle.oss.mysql.mysqld.plist'. don't have one? (download one such as vim,sublime,etc)

4. Copy the line below to the secotion ProgramArguments, **Save and Restart Your Mac**.
```
<string>--secure-file-priv=/usr/local/mysql</string>
```
![](https://qixing810.github.io/content/post/error1290/gallery/2.jpg)

5. go back to step 1 to check again, if you no longer see anything like `null` or `/`, then congratulation!
![](https://qixing810.github.io/content/post/error1290/gallery/3.jpg)

6. you need to upload your excel, csv or other files in this directory though:
```
/usr/local/mysql
```

7. Enjoy no more error code 1290.



<br>
Reference:<br>
https://stackoverflow.com/questions/40561248/trying-to-import-files-into-mysql-5-7-16-got-error-code-1290-secure-file