#### conf/local.conf (or) local.conf.sample in your own layer
---

###### Enabling Build History

If you enable build history, yocto will save the build history of packages in a local git repository allowing you to compare the changes you did to a package.

```
INHERIT += "buildhistory"
BUILDHISTORY_COMMIT = "1"
```

###### Removing Build Output

* Removing whole build output
```
INHERIT += "rm_work"
```

* Removing specific packages
```
RM_WORK_EXCLUDE += "linux-yocto u-boot"
```

* By default previous images are not erased. To erase previous images
```
RM_OLD_IMAGE = "1"
```


###### Changing BBAPPEND As Warning Instead of Error

`BB_DANGLINGAPPENDS_WARNONLY = "true"`



