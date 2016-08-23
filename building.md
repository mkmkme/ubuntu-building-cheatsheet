# Ubuntu building cheatsheet
**!** You must have `DEBEMAIL` and `DEBFULLNAME` to be set **!**

**!** Make sure to have `~/.quiltrc` file or at least export
`QUILT_PATCHES=debian/patches` variable **!**

```sh
mkdir some-package # I don't want to pollute my cwd
apt-get source some-package
cd some-package
# Create patch somehow
cp path-to.patch debian/patches
quilt import debian/patches/my-patch.patch
dch -i # Fix version and describe your changes
debuild -S
dput ppa:<your-ppa> ../some-package.changes
sudo apt-get build-dep some-package
dpkg-buildpackage -rfakeroot
cd ..
dpkg -i some-package.deb
```
