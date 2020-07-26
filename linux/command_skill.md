# Command Skill

## pushed popd
切換dir

## rsync
```
rsync -av --delete /cygdrive/d/from_dir/ /cygdrive/d/to_dir/ --exclude=.svn --exclude=tmp --exclude=log
```

## 檔名加時間
```
myfile_`date '+%F_%T'`.txt
```

## awk and xargs
```
ps -ef | grep '/usr/bin/ssh' | awk '{print $2}' | xargs kill -9;
```

## grep 正則
```
正則
grep "^\[2015\/11\/07" development.log > tmp.log
```

## curl
