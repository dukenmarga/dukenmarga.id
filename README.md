Blog https://dukenmarga.id using Hugo.

## Install Hugo

Installation steps for local development

```
sudo zypper addrepo --refresh https://download.opensuse.org/repositories/system:/snappy/openSUSE_Leap_15.4 snappy
sudo zypper --gpg-auto-import-keys refresh
sudo zypper dup --from snappy
sudo zypper install snapd
sudo systemctl enable snapd
sudo systemctl start snapd
sudo systemctl enable snapd.apparmor
sudo systemctl start snapd.apparmor
sudo snap install hugo

snap run hugo server --minify
```

Since we use themes using git submodules, update all submodules before build the docker in production server. See here for details.

```
git submodule update --init --recursive     # only first time on new server
git submodule update --recursive --remote   # update themes on regular basis
```


## Resource

Hugo
- https://gohugo.io/getting-started/quick-start/

Hugo Theme:
- https://github.com/xianmin/hugo-theme-jane
- https://www.xianmin.org/hugo-theme-jane/

