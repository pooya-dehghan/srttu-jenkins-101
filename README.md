# srttu-jenkins-101

این مخزن یک اموزش ابتدایی برای راه اندازی جنکینز روی سرور لینوکسیه ! مختص بچه های شهید رجایی و دانشکده مهندس کامپیوتر ! زنده باد نرم افزار و متن باز !

## نیاز اولیه
- سرور لینوکس

- داکر

- گیت و گیت هاب

- مقدار کمی علاقه!

# شروع کردن 
- خرید یک سرور خارج از کشور !
  
 پیشنهاد میکنم که یک سرور خارج از کشور تهیه کنین بهتره که المان باشه ! این سرور هارو ارایه دهنده های محترم مثل آروان ، پارس پک و ... میفروشن و میتونین تهیه کنین!
شما حداقل نیاز هایی که برای سرور دارین طبق داکیومنت خود جنکینز سروری با رم 2 و حداقل 10 گیگ فضای ذخیره سازی هست پس جای نگرانی زیادی نیست و میتونین حداقل سرور هارو خریداری کنین

 حتما و حتما رمز و یوزرنیم برای دسترسی به سرور خودتون رو عوض کنین و از پیشفرض استفاده نکنین ! برای عوض کردن رمز میتونین داخل لینوکس کامند پایین رو اجرا کنین : 
 ```shell
sudo passwd root
```

-داکر

در ادامه مطمن بشین که داکر روی سرور لینوکسی شما نصب باشه !  برای اینکه مطمن بشین که داکر نصبه از دستور زیر استفاده کنین : 
 ```shell
docker -v
```

اگر که نصب باشه داکر و ورژنش رو به شما میگه اگر نه باید زحمت نصب داکر و داکر کمپوز رو به خودتون و سرور خارج از کشورتون بدین :)) 

(https://docs.docker.com/engine/install/ubuntu/)

لینک بالا برای نصب و راه اندازی داکر روی ابونتو هست اما نگران نباشین برای همه توزیع های لینوکسی میتونین اموزش مربوطه رو پیدا کنین و انجام بدین !


 ```shell
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

خب ابتدا با این دستور هرچی که از داکر قبلا نصب کردین رو پاک کنین و تمیز کنین سرورتون رو !!


 ```shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

سپس با استفاده از این دستور کلید gpg رو نصب کنین برای داکر بعدش هم پکیج های مورد نیاز رو نصب کنین داخل سرورتون


 ```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

حالا با پکیج منیجرتون داکر رو نصب کنین و با دستور -v بالا که بهتون گفتم مطمن بشین که داکر نصب شده !

-جنکینز 

حالا بریم سراغ نصب جنکینز و بالا اوردنش با استفاده از داکر !


 ```shell
docker network create jenkins
```

دستور بالا براتون یک نتورک از جنس bridge میسازه که داخل اون باید کانتینر های مربوط به جنکینز رو ران کنین و ازش استفاده کنین.



 ```shell
docker run \
  --name jenkins-docker \
  --rm \
  --detach \
  --privileged \
  --network jenkins \
  --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind \
  --storage-driver overlay2
```

این دستور براتون یک ایمیج یا تصویر از داکر دی ای ان دی میسازه که شما میتونین داکر رو داخل یک کانتینر داشته باشین !! 

حالا برین یک دایرکتوری که دوست دارین و یک Dockerfile درست کنین و این دستورات رو توش قرار بدین
 ```shell
FROM jenkins/jenkins:2.426.2-jdk17
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"
```

بسیار خب الان باید یک ایمیج از این  داکر فایل درست کنیم ....

```shell
docker build -t myjenkins-blueocean:2.426.2-1 .
```

با استفاده از این دستور شما میتونین یک ایمیج به قول معروف بیلد کنین !

الان با استفاده از دستور های زیر وضعیت داکر کانتینر ها و ایمیج هارو چک کنین 

```shell
docker ps

docker images
```
الان وقتشه که از روی این ایمیجی که ساختیم یک کانتینر بیاریم بالا و به جنکینز دسترسی پیدا کنیم ! 


```shell
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.426.2-1
```

خب الان میتونین به پنل جنکینز خودتون با ادرس سرور و همچنین در پورت 8080 دسترسی داشته باشین
توجه کنین فقط که باید رمز  رو از مسیر زیر دربیارین :

```shell
 /var/lib/jenkins/secrets/initialAdminPassword
```

