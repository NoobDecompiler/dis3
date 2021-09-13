### dis3
Disasembler and assembly python source code. only for python 3.9
### sekilas info!
tools ini diutamakan untuk platform Linux `aarch64` ya bre.
jadi kalo platform lu bukan Linux `aarch64` kemungkinan emang gak bisa.
jadi, kalo gk bisa di hp lu, jangan tanya ke gw ya bre😆, gw harap lu paham.
lu bisa cek info plaform lu dengan cara ketik perintah berikut di termux.
````bash
$ uname -m
````
kalo hasilnya bukan `aarch64` gak usah di install tools ini, okeh.
#
install tools ini dengan command berikut!
````bash
$ dpkg -i dis3_1.0_aarch64.deb
````
cara make nya gimana?
begini...
````bash
$ dis3 [mode] [file]
````
#
contoh penggunaan mode `dis` untuk unpack code.
#
berikut ini penjelasan
untuk unpack code gunakan mode `dis` contoh sebagai berikut
````bash
$ dis3 dis [file]
````
untuk `[file]` isi aja dengan nama file extensi `pyc` atau `py`.
#
dan biar gak ribet² nyalin sana sini gunakan `> output file` agar hasil unpack langsung ke simpen.
#
contohnya kayak berikut ini!
````bash
$ dis3 dis file.pyc > save.dis
````
untuk melihat atau mengedit file hasil unpack tinggal pake `nano` aja bre.
#
contoh penggunaan mode `asm` untuk membangun ulang kode hasil unpack mode `dis`.
#
caranya kurang lebih sama kayak penggunaan mode `dis`. tapi yg ini gak usah make `> output file`.
#
cukup seperti berikut.
````bash
$ dis3 asm save.dis
````
`save.dis` adalah nama file hasil unpack dari file `file.pyc`. yah lu ngerti lah maksud gw.
#
dan jika berhasil maka akan terbuat file baru dengan nama `save.pyc`.
#
kurang lebih begitulah penjelasannya, kalo ada bug atau eror di tools nya, harap lapor ke whatsapp gw ya bre😄
#
whatsapp me: [0812...](https://wa.me/+6281210160358)
#
okeh cukup sekian dan terimakasih telah membaca walaupun cuma dalam hati!


