## 在SourceTree 使用兩組SSH Key
*** 
使用github, gitlab等平台時，需要給帳號設置一組SSH Key，可以參考這[官方教學][1]． 

但如果想在同台電腦上使用兩組以上帳號 (SSH key) push到遠端不同的平台, 預設都會使用id_rsa，這時候該如何指定呢？

假設已經有了一組工作使用的帳號，現在要再新增一租私人用的

1. 為私人帳號新增一組SSH Key，存成一個新檔名 : id_rsa_private

    ```
    $ ssh-keygen -t rsa -C "account@example.com"
    ```

2. 把key加到ssh agent

     ```
     $ssh-add ~/.ssh/id_rsa_private
     ```

3. 添加到github上，[官方教學][1]

     ```
     $ pbcopy <~/.ssh/id_rsa_private.pub
     ```

4. 再來就是配置多個SSH Key，分別指定對應的key．

    ```
    $ vi ~/.ssh/config
    ```    
    內容如下 :

    ```
    Host example-gitlab.example
      HostName example-gitlab.example
      IdentityFile ~/.ssh/id_rsa''

    Host github.com
      HostName github.com
      IdentityFile ~/.ssh/id_rsa_private      
      ```

 完工！這樣就可以在分別的repo更改，會自動對應相對的SSH Key了．


[1]: https://help.github.com/articles/generating-an-ssh-key/ "官方教學"