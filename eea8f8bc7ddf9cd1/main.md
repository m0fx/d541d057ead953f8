# The JeeWMS-v3.7 system has a background SSTI vulnerability that causes RCE

  JeeWMS version : < = v3.7, vulnerable to background SSTI attacks, allowing attackers to execute remote commands.
  
  Project source code address:https://gitee.com/erzhongxmu/JEEWMS

#### Step 1:
  Through the configuration file ' pom.xml ' file, it can be seen that the back-end uses the freemarker template framework. So make a template file with payload and compress it.

```
# payload
<#assign value="freemarker.template.utility.Execute"?new()>${value("cmd.exe /c calc")}
```

![2025-05-06-164509](./src/img/2025-05-06-164509.png)

![2025-05-07-161329](./src/img/2025-05-07-161329.png)

#### Step 2:
  After the JeeWMS system is deployed locally, it enters the system background.

![2025-05-06-164009](./src/img/2025-05-06-164009.png)

#### Step 3:
  Find the 'Online表单样式' function in the '在线开发' column in the left function bar and open it.After opening, click the '录入' button to create a new form style.

![2025-05-06-164729](./src/img/2025-05-06-164729.png)

#### Step 4:
  Click '浏览文件' at the '上传风格模板' of the creation interface to select the prepared template archive file and click the '确定' button to upload.

![2025-05-07-010535](./src/img/2025-05-07-010535.png)

#### Step 5:
  After the upload is completed, open the 'Online表单开发' function, tick any form, and click the '编辑表单' button. Then select the previously created style template in the open interface 'PC表单风格'.

![2025-05-07-000106](./src/img/2025-05-07-160519.png)

![2025-05-07-160806](./src/img/2025-05-07-160806.png)

#### Step 6:
  After saving the modifications, click the '功能测试' button of the corresponding form, and then click the '录入' button to trigger the payload completion command execution.

![2025-05-07-160520](./src/img/2025-05-07-160520.png)

![2025-05-07-160900](./src/img/2025-05-07-160900.png)

![2025-05-07-011148](./src/img/2025-05-07-011148.png)

#### Demo video
http://47.99.62.25:47619/JeeWMS-SSTI.mp4

