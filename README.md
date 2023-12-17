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



