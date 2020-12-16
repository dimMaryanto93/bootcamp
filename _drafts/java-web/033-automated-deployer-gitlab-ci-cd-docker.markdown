---
layout: post
title: "Automated deploy with gitlab CI/CD"
lang: java-web
categories:
- java
- web
- war
refs: 
- http://tomcat.apache.org/
- https://codehaus-cargo.github.io/cargo/Maven2+plugin.html
- https://docs.gitlab.com/ce/ci/
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
comments: true
image_path: /resources/posts/java-web-033
---

Automation deployment / delivery object sebetulnya ada beberapa cara dan tools contohnya seperti:

1. [Jenkins](https://www.jenkins.io/)
2. [Jebraint Team City](https://www.jetbrains.com/teamcity/)
3. [Github Action](https://github.com/features/actions)
4. [Travis CI](https://travis-ci.org/)
5. [Gitlab CI/CD](https://docs.gitlab.com/ce/ci/)

Nah di materi kali ini saya akan menggunakan `Gitlab CI/CD` karena ada beberapa alasan sih

1. Gitlab ecosystem, udah lumayan lengkap dan yang pasti gratis.
2. Bisa di install pada server sendiri (on premise)
3. Script deploymentnya menjadi satu dengan project. ini kebiasaan aja sih klo saya emang biasanya lebih sering pake gitlab ketimbang yang lain.

Ok sekarang kita buat script deployment di gitlab ci/cd. dengan cara buat file dalam root project dengan nama `.gitlab-ci.yml` seperti berikut:

{% gist page.gist ".gitlab-ci.yml" %}

Jadi disini saya menggunakan `docker-executor` di `gitlab-runner` jadi semua service jalan di dalam container docker. 

Image yang digunakan untuk melakukan build project ini yaitu [maven:3.6.3-jdk-8](https://hub.docker.com/_/maven).

Variables, ada beberapa variable yang kita perlu set di `Setttings` -> `CI/CD` ->` Variables` seperti berikut:

![gitlab ci/cd]({{site.baseurl}}{{page.image_path}}/gitlab-ci-cd-variables.png)

dan untuk property `only` => `/-release/` ini tujuannya adalah ketika kita push pada branch / membuat tag dengan prefix tersebut akan automatis di jalankan command script nya.

OK, setelah itu kita commit dan push. dengan perintah seperti berikut:

{% highlight git %}
# index file .gitlab-ci.yml
git add .gitlab-ci.yml

# commit file
git commit -m "script deployment"

# push code
git push 

# create tag 
git tag -a 2020.12.16.22.23-release -m "first deploy"

# push tag
git push --tags
{% endhighlight %}

Kemudian kita coba check pada menu `Pipeline` hasilnya seperti berikut:

![git build]({{site.baseurl}}{{page.image_path}}/gitlab-build-success.png)