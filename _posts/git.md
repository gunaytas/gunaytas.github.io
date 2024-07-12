---
layout: post
title: Git ve Git komutları
subtitle: Git nedir? Git kullanımı ve komutları
# cover-img: /assets/img/path.jpg
# thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [git]
author: Günay TAŞ
---


Configuration -> Kullanıcının bilgilerini ayarlamak, tanıtmak için kullanılır. Genellikle Git kurulumundan sonra yapılır, tekrar yapılmasına gerek kalmaz.

```shell
git config --global user.name "kullanıcıadı"
```
```shell
git config --global user.email "kullanıcımaili"
```

```shell
git config —list
```
Tutulan konfigürasyon bilgilerini kontrol etmek için kullanılır.

```shell
git init
```
Bu komut ile yerel depolama alanında .git klasörü oluşturulur. .git klasörü altında yeni repository için gerekli metadatalar tutulur. Tek seferlik bir işlemdir. Önceden var olan bir projeyi ilk kez Git ile versiyon kontrolü yapmak için veya boş bir projeyi Git ile kontrol edebilmek için kullanılır.

```shell
git clone ssh://john@example.com/path/to/my-project.git
```
Repository dosyalarını yerel depolama alanına kopyalamak için kullanılır.

```shell
git status
```
Git değişiklik yapılan dosyaların takibini yapar. Yeni veya değişiklik yapılmış dosyaların stage bilgilerini listeler. 

```shell
git add .
```
Bütün dosyaları commit etmek için staging alanına ekler. Dosya adı belirtilirse sadece belirtilen dosyayı ekler.

```shell
git commit -m “First Commit”
```
Staging alanındaki dosyaları remote repoya işlemek üzere yerel dizinde kaydeder. Çift tırnak içerisinde mesaj belirtilir. Özellikle değiştirilmediği sürece değişmez. Projenin güvenli versiyonları olarak düşünülebilir.

```shell
git push origin main
```
Yerel dizindeki commit edilen dosyaları remote repoya ekler.

```shell
git diff
```
Versiyonlar arasında değişen alanları gösterir.


Branch(dal), repository'nin branch'i oluşturulan zamandaki güncel olan bir kopyasıdır. Ana kodu etkilemeden branch üzerinde çalışma imkanı sağlar. İstenildiği zaman yapılan değişikliklerin ana koda eklenmesine izin verilir.

```shell
git branch feature
```
feature isimli yeni bir branch oluşturur. Oluşturulan branch’e geçiş yapmaz.

```shell
git checkout -b feature
```
feature isimli yeni branch oluşturur. Oluşturulan branch’e geçiş yapar.

```shell
git checkout main
```
main isimli branch’e geçer.


```shell
git pull origin feature
```
Remote repoda bulunan değişiklikleri yerel dizine çeker.


```shell
git merge
```
Farklı branchlerdeki değişiklikleri birbirine entegre etmek için kullanılır.


```shell
git log
```
Yapılan commitlerin bilgilerini listeler.


```shell
git branch -d <branch>
```
Belirtilen branch’i yerel dizinden silmek için kullanılır.


```shell
git push origin --delete crazy-experiment
```
Belirtilen branch’i remote repodan silmek için kullanılır.


```shell
git revert 14a649d25367e2c10f7e30ec6617c98fb3237ece
```
Yapılan değişikliği geri almak için kullanılır. Commit ID yazılır.


```shell
git reset --hard fb47626f2c562e12a49a8d86f421406765b04afa
```
commiti geri alma


```shell
git rebase
```

