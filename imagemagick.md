## Instalar o ImageMagick

```
sudo apt-get install libjpeg62 libjpeg62-dev

wget ftp://ftp.imagemagick.org/pub/ImageMagick/ImageMagick.tar.gz
tar xvfz ImageMagick.tar.gz
cd ImageMagick-*
./configure --disable-shared
make
sudo make install
ldconfig /usr/local/lib
```

Also after you run the command ./configure --disable-shared, look at the last 50 lines and make sure you see;

JPEG v1           --with-jpeg=yes       yes
JPEG-2000         --with-jp2=yes        yes

If it says no then you need to install libjpeg62 and possibly libjpeg62-dev. That worked for me, hope it helps others.

Fonte: https://serverfault.com/a/202737


## Resize in batch

```
for file in convert PATH/*.jpg; do convert $file -resize 50% $file; done
```
