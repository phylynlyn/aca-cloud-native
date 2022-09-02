# Container for new Starter(1)
`Academy kakkai by Saritrat Jirakulphondchai aka P’JoJo`

## VM ? Container?
Container และ VM นั้นไม่ได้มีการเอามาแทนที่กันแต่อย่างได้แต่นำมาใช้ร่วมกัน optimize ซึ่งกันและกัน

Virtual Machine aka VM — เครื่องเสมือนสร้างขึ้นมาเพื่อตอบโจทย์ในเรื่องของการ scale
Container — ตอบโจทย์ในเรื่องของ Utilize Resource, build once run anywhere
มุมมองต่อ Container
Developer: build ครั้งเดียว run ได้ทุกที่

Devops: configure การทำ life cycle ทำครั้งเดียว run ได้ทุกที่

## Container คืออะไร?

“คอนเทนเนอร์” (container) เป็นเทคนิคในการจัดการ package software ประเภทหนึ่ง นิยามของ Containers เปรียบเสมือนตู้ Container ที่อยู่บนเรือที่สามารถยกเข้า/ยกออกได้ เมื่อมีการ build หรือใส่ของเข้าไปเเล้วเราจะไม่สามารถเเก้ไขของข้างในได้สิ่งนี้เรียกว่า “ตัวต้นแบบ” หรือว่า Container Image ทำให้แน่ใจได้ว่าไม่ว่าจะนำไปใช้ที่ไหนก็จะเป็นของสิ่งๆเดียวกัน ยุคเเรกๆ เรามักจะเจอเป็น หาการ ใช้ library หลายๆ version ชนกัน Container จะมาช่วยแก้ปัญหาในส่วนนั้น

แล้วอะไรที่เราควรนำไปใส่ใน Container บ้างหล่ะ ทุกอย่างเลย ยกเว้น?

static files เราจะไม่นิยมใส่เข้าไป เพราะ static files จำเป็นที่จะต้องมีตัวนำทางไปเปิด html (reverse proxy) static files ไม่มี state อะไรเลยนอกจากทำหน้าที่ในการ run แล้วก็จบ ไม่ต้องมี server on cloud จะนิยมนำไปใส่ blob storage, S3, Data lake


แล้ว “static files” คืออะไรใน term ของ web application (Frontend)

Code (Human Language)(1) -> Compile/ Transpile/ Interpret(2) -> Machine Code(3) -> Running / Process(4)

Client Side Rendering (CSR) ใช้เครื่อง Client ในการ Render .html (ผ่าน browser)
Server Side Rendering (SSR) render ที่ server แล้วมีการส่ง .html กลับมา
Static Site Generation (SSG) ไม่มีการ render คือเป็น file .html เปล่าๆ
สิ่งที่ไม่มีการ render และไม่มีการส่ง .html กลับมา เรียกว่า “static files”

## Docker คือสิ่งที่เราจะมาเรียนรู้ในวันนี้


Docker คืออะไร มันคือ Container Runtime Engine ตัวหนึ่งเอาไว้ run container และ build image ซึ่งกระบวนการ การนำของเข้าไปใน container -> containerization



จาก Docker Overview ข้างบนจะเห็นได้ว่ากระบวนการหลักจะหนีไม่พ้น 4 ขั้นตอน

`Dockerfile`: ไว้ระบุการทำงาน (Build) คำนิยาม คือ Set of instructions to build a container image
`Image`: ตัวต้นแบบเมื่อสร้างขึ้นมาเเล้ว (Ship) คำนิยาม คือ A read-only template
`Registry`: โรงเก็บ หรือ container registry (Run) คำนิยาม คือ Stores, distributes and manages Docker images
`Container`: Container Instance คำนิยาม คือ Runnable instance of an image

## Docker Command
หรือ คำสั่งของ Docker CLI

`dockerbuild`
คือ command ในการสั่ง docker server ให้มันไปสร้าง image จาก dockerfile แล้วไปเก็บไว้ใน container registry local หรือ เครื่องของเรา



syntax
```$docker build -t <image-name>:<tag> <directory>```

(-t):tag: ถ้าเราไม่ระบุมันจะใส่ latest เป็น default เสมอ

directory: context ที่ dockerfile อยู่



ถ้าเราจะ build อะไรสักอย่างเราต้องเตรียม set of instruction ของ dockerfile เพื่อไปสร้าง container image และ ไปเก็บ อยู่บน local registry

`dockerImage`
คือ command ไว้ list image ทั้งหมดที่อยู่บนเครื่องเรา

syntax
```$ docker images```

# Contaner Registry
aka โรงเก็บ หรือ ที่เก็บ

มี 2 ประเภท
- local
- public

`dockerpull`
คือ command ที่ช่วยในการ pull หรือดึง image จาก public registry มาที่ local registry ของเรา

syntax
```$ docker pull python:3.9.6```

`dockerrun`
คือ command ที่จะช่วยในการ run Docker หรือ clone ไปเป็น container instance

syntax
```$ docker run -d -p <server-port>:<container-port> <image-name>:<tag>```

(-d):deamon mode: คือการสั่งให้ทำงานเบื้องหลัง

(-p):port: คือช่องทางในการเข้าออก

หลังจาก build container image มาเก็บที่ local แล้วเราจะเอาของขึ้นไปเก็บ บน cloud ยังไง?

`dockerpush`
คือ command เพื่อนำของไปเก็บบน cloud

syntax
```$ docker push <image-name>:<tag>```

`docker ps`
คือ command ในการเช็คของหรือ container instance

syntax
```$ docker ps <option>```

ถ้าพิมตรงๆโดยที่ไม่ใส่ option มันจะ list process ที่ทำงานอยู่ แต่ถ้าใส่ -a ไปด้วยมันจะเอาที่เคยทำ ที่ตายไปแล้ว ขึ้นมาเเสดงด้วย

`docker logs`
คือ command ใช้ในการเช็ค logs ของ application ที่อยู่ใน container

syntax
```$ docker logs <container-id> <option>```

`docker exec`
คือ command ในการกระโดดเข้าไปใช้งานใน container แต่ถ้าเรา exec เข้าไปต้องมี kernel ให้กระโดดเข้าไป

syntax
```$ docker exec -it <container-id> <shell>```

e.g.

```$ docker exec -it abc234we4 bash```

```$ docker exec -it abc234we4 sh```

Session ต่อไป จะเป็น เรื่อง Dockerfile การทำ multistage สำหรับตัว Container for new starter(1) ก็ขอจบเพียงเท่านี้ขอบคุณครับ