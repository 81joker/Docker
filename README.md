
# docker --help

# dokcer network --help
    # docker network create --help


Container ( container com from image and image come from hup ) !
# docker container --help

    This to make the first Container to me 
    # docker container create hello-world:linux
        # 
        Unable to find image 'hello-world:linux' locally
        linux: Pulling from library/hello-world
        e6590344b1a5: Pull complete 
        Digest: sha256:a77ecd852b17bfaee6708208960645d20fc9e6d0eec12353f8eb0e7b94bb647a
        Status: Downloaded newer image for hello-world:linux
        7af9489380f3cb35037761e0d2ce948fa167970bcc9544d36b27b1bce8fe899c

        Unable to find image 'hello-world:linux' locally
        تعني أن Docker لم يجد الصورة محليًا.
        بعدها:
        linux: Pulling from library/hello-world
        e6590344b1a5: Pull complete
        تعني أن Docker قام بتحميل الصورة بنجاح.
        الـ Digest هو رقم فريد يمثل الصورة.
        وأخيرًا:
        Status: Downloaded newer image for hello-world:linux
        7af9489380f3cb35037761e0d2ce948fa167970bcc9544d36b27b1bce8fe899c

        إذا أردت تشغيل الحاوية، تحتاج إلى استخدام:
        docker container start <container-id>


# docker ps --all

# dokcer logs ID
بعد إنشاء الحاوية (container) وتشغيلها، قد تحتاج إلى عرض السجلات (Logs) الخاصة بها.
# dokcer logs (first 3 from Id ) 7af

docker container attach <container-id>


# docker build --help 
 display alot of the options i choose 
 # docker build -t our-first-image . 
      [+] Building 0.1s (1/1) FINISHED                           docker:desktop-linux
        => [internal] load build definition from Dockerfile                       0.0s
        => => transferring dockerfile: 2B                                         0.0s
        ERROR: failed to solve: failed to read dockerfile: open Dockerfile: no such file or directory

        View build details: docker-desktop://dashboard/build/desktop-linux/desktop-linux/e8qfttp4djtz5la35f0jb1hoi
    # Then i Run: # dokcer run our-first-image

NOT: dokcer run = dokcer container create + docker container strat + dokcer container attach


# https://docs.docker.com/build/exporters/

# https://docs.docker.com/build/BuildKit

ما هو Docker BuildKit؟
BuildKit هو نظام بناء حديث تم تقديمه من Docker لتحسين تجربة بناء الصور (Images). تم تصميمه ليكون أسرع، أكثر كفاءة، وقابلية للتوسعة مقارنةً بالنظام التقليدي.

# المزايا الرئيسية لـ BuildKit

- **أداء بناء أسرع**  
  يستخدم BuildKit أساليب متقدمة مثل تنفيذ الأوامر بالتوازي (Parallel Execution) وتحسينات في إدارة التخزين المؤقت (Cache).

- **إدارة متقدمة للتخزين المؤقت (Cache)**  
  إمكانية استخدام التخزين المؤقت من صور أو مراحل سابقة.  
  دعم لتصدير واستيراد التخزين المؤقت.

- **دعم أسرار البناء (Build Secrets)**  
  إمكانية تمرير أسرار أثناء عملية البناء بدون تضمينها في الصورة النهائية.

- **دعم الوصول للـ SSH**  
  يمكنك تمرير مفاتيح SSH للبناء عند الحاجة للوصول إلى مستودعات خاصة مثلاً.

- **المخرجات المتعددة (Multi-Output)**  
  بناء عدة مخرجات من نفس الـ Dockerfile في نفس العملية.

- **التنفيذ المتوازي لعدة مراحل (Parallel Build Stages)**  
  تحسين وقت البناء من خلال تنفيذ المراحل بشكل متوازي إن أمكن.

- **دعم للـ Frontends المخصصة**


# [builders/drivers](https://docs.docker.com/build/builders/drivers/)
    ما هو Buildx Driver؟
    عند استخدامك للأداة docker buildx، فإن عملية البناء تتم عبر وحدة تُسمى Builder Instance، وهذه الوحدة تعتمد على Driver.
    الـ Driver يحدد كيفية تنفيذ عمليات البناء وأين سيتم تشغيلها.

    ببساطة:

    الـ Driver = الطريقة أو البيئة التي يستخدمها BuildKit لتنفيذ عملية البناء.


# docker ps -aq | xargs 
# docker rmi -f 
# docker build -t our-web-nehad -f web-server.Dockerfile .
      docker build: This tells Docker you want to build an image—kind of like creating a software package based on instructions.

    -t our-web-server: The -t flag names (or tags) your image. In this case, you're calling it our-web-server, so you can easily refer to it later.

    -f web-server.Dockerfile: This specifies the Dockerfile you want to use. By default, Docker looks for a file named Dockerfile, but here you’re explicitly telling it to use web-server.Dockerfile instead.

    . (dot): This is the build context—the directory Docker will use when sending files to the Docker daemon. The dot means “current directory.”

# docker run --rm --entrypoint sh ubuntu -c "echo 'Hello there.' > /tmp/file && cat /tmp/file"
        --rm
        Automatically removes the container once it finishes running. This keeps your system clean by not leaving stopped containers behind.

        --entrypoint sh
        Overrides the default entrypoint (the default command that Ubuntu would run) and sets it to sh (the shell). This means we are explicitly telling the container to execute a shell command.

        ubuntu
        This is the Docker image used. It tells Docker to pull and run the official Ubuntu image.

        -c "echo 'Hello there.' > /tmp/file && cat /tmp/file"
        This part is passed to sh -c and is the actual shell command that gets run inside the container:

        echo 'Hello there.' > /tmp/file
        Writes the text Hello there. to a file at /tmp/file.

        &&
        Runs the next command only if the previous one succeeded.

        cat /tmp/file
        Reads and displays the contents of /tmp/file — which should be Hello there..

[🧾 What It Does in Practice]
  Starts an Ubuntu container.

  Writes "Hello there." to /tmp/file.

  Prints the contents of /tmp/file to the terminal.

  Deletes the container after it exits.


# mkdir -p ~/docker_share
# touch ~/docker_share/file.txt
# docker run --rm --entrypoint sh -v ~/docker_share/file.txt:/tmp/file ubuntu -c "echo 'Hello there.' > /tmp/file && cat /tmp/file


# docker system prune 
# docker system prune -a
    🧹 ما هو docker system prune؟
    هو أمر يقوم بـ:

    حذف الحاويات المتوقفة (stopped containers)

    حذف الشبكات غير المرتبطة (unused networks)

    حذف الصور غير المستخدمة (dangling images)

    حذف الكاش الخاص بـ build
# docker rmi 
# docker kill

# docker run --name=alpine --entrypoint=sleep -d alpine infinity
  --entrypoint=sleep	تشغيل أمر sleep كمدخل رئيسي بدلاً من sh أو ash
  -d	تشغيل الحاوية في الخلفية (Detached mode)
  alpine	اسم الصورة (الخاصة بـ Alpine Linux)
  infinity	وسيطة لـ sleep تعني "نوم إلى الأبد"

#  docker exec -i -t nameImage sh

# docker exec -d alpine sleep infinity
# docker top alpine
 
# docker context ls
# docker context use imageExample  

# docker rmi -f $(docker images -aq)
  To delete all the images,

# docker rm -vf $(docker ps -aq)
  To delete all containers including its volumes use,


<!--   To Search for Image  -->
# docker search python or php or npm or java
# docker search --filter is-official=true python or php or npm or java

<!-- You can find the min of starts  -->
# docker search --filter stars=100  python or php or npm or java


<!-- You can use this to search for automated Docker images of popular languages -->
# docker search --filter is-automated=true python or php or npm or java


<!-- List all Docker images for Python with full descriptions -->
# docker search --format "{{.Name}}: {{.Description}}" --no-trunc python


<!-- List all Docker images, including intermediate and unused ones -->
# docker image ls --all

<!-- List all Docker images with full output, avoiding truncation -->
# docker image ls --no-trunc

<!-- List all Docker images showing only their IDs -->
 # docker image ls --quiet

<!-- List all Docker images along with their digests -->
# docker image ls --digests


<!-- Search Docker Hub for images with names starting with "python" -->
# docker search python

# List local images created before the 'python' image
## docker image ls --filter before=python

# List Docker images created after the 'python' image
## docker image ls --filter since=python

# List all dangling Docker images (untagged and unused)
## docker image ls --filter dangling=true









