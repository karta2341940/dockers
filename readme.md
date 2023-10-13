# How to use
在當前目錄下打開 powershell or cmd 並且執行 `docker compose up -d`
就會在背景執行兩組wordpress和mysql
如需要測試可將hosts設定為
```
127.0.0.1 test1.nptu.edu.tw
127.0.0.1 test2.nptu.edu.tw
```
並且在瀏覽器輸入 `test1.nptu.edu.tw` 和 `test2.nptu.edu.tw` 即可看到兩個wordpress
# 增加網站
如果需要增加網站的話需要在docker-compose.yml中增加一組wordpress和mysql
，並於nginx.conf/setting中增加一個新的conf檔案，在至docker-compose.yml中的nginx服務下將新的conf檔案bind mount進去


# 備註
目前的實作方式為使用一個nginx服務來依網址轉發到不同的wordpress服務，
並且wordpress的volume如需要備份需額外自行備份。另外如果需要連線至DB可以將db的port外開，這樣即可用mysql workbench連線至DB，或是可嘗試將mysql workbench的image加入docker-compose.yml中，並且將network設定為wordpress的network，這樣就可以直接在mysql workbench中連線至DB了。

## wordpress 預載插件
這部分需要自行基於wordpress的image進行修改，大致上是撰寫一份符合自己需求的dockerfile，並且build起來，然後在docker-compose.yml中將wordpress的image改為自己的image，這樣就可以達到預載插件的效果了。