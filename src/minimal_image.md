#### USING SYSTEMD AS INIT SYSTEM INSTEAD OF INIT
---

* Copy these lines in your conf/local.conf
```
DISTRO_FEATURES_append = " systemd"
VIRTUAL-RUNTIME_init_manager = "systemd"
DISTRO_FEATURES_BACKFILL_CONSIDERED = "sysvinit"
VIRTUAL-RUNTIME_initscripts = ""
```

**NOTE**: Don't miss the space in  `DISTRO_FEATURES_append`

**NOTE**: Remove `tmp` folder incase you already have a built image


