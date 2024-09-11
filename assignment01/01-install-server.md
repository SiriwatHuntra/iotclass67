# Install Server and Docker


## How to install Server

    วิธีการ install Server (เข้าใจว่าคือ Ubuntu Server) เริ่มด้วยการเปิดเครื่องคอมพิวเตอร์ที่เราจะใช้งานก่อน โดยเราจะใช้ 
    Dell Edge Gateway 5000 เป็นเครื่องหลักในการทำงานต่างๆรวมไปถึงการลง Server และต่อ IoT โดยเมื่อเรา Setup Work Enviroment แล้ว (ในกรณีนี้คือการเปิดเครื่องเชื่อมจอ, Keyboard แล้ว) เราก็ต้องทำการลง Ubuntu Server โดยเราจะใช้ Version 22.04 และทำการลงโดยใช้ USB Stick ในการลง OS ซึ่งเราก็ต้องทำให้ USB Flash Drive นั้น เป็น FAT32 ก่อนด้วยโดยแนะนำให้ใช้ Program Rufus จะทำให้ทุกอย่างงานขึ้นมาก และหลังจากนั้นก็ทำการลง OS ตามปกติเหมือนกับการลง Windows OS ตามลำดับ 

    โดยการลง Ubuntu Server ใน Dell Edge Gateway 5000 ต้องเป็นการลงแบบ Minimun Installation
    ไม่อย่างงั้นอาจจะเกิดปัญหาในการทำงานได้
    และต้องจัดการ Partition ในเครื่องให้ดี
    Networking ก็ต้องทำให้ดีด้วยเช่นกัน Set IP ในเรียบร้อย และต้องเป็น Static IP ด้วย
    ถ้ามี SSH ให้ลงตอน Install Ubuntu ให้ทำการ Install ไปด้วย

    และเมื่อได้ทำการลง OS เสร็จเรียบร้อยแล้วก็ให้ทำการ Update และ Upgrade ให้เรียบร้อย โดยในขั้นตอนนี้อาจจะต้องมีการเชื่อมต่อ Internet ด้วยเพื่อให้ Ubuntu Server เราสามารถ Update และ Upgrade ได้ โดยมีหลายวิธีแต่เรานั้นใช้วิธีการส่ง Internet จาก Notebook นึงไปยัง Ubuntu Server เราโดยใช้การ Bridge Connection เอา
    ถ้ามีความสามารถและอุปกรณ์มากพอ ให้ทำการใช้ Switch ต่อ LAN ที่มี Internet และ ให้เชื่อมต่อ Access Point เข้ากับ Switch และ Set Access Point และ Switch ให้เรียบร้อย จากนั้น
    ให้เชื่อมต่อ Gateway Server เข้ากับ Switch และทำการเชื่อมต่อเข้าให้งาน Server ผ่าน Wireless จาก Access Point โดยใช้การ SSH เข้าไป

    ตอนนี้ Ubuntu Server เราก็ควรที่จะพร้อมต่อการลงเครื่องมือต่างๆแล้ว

## How to install Docker

    https://docs.docker.com/engine/install/ubuntu/

    สามารถทำตามเว็บ Offical ได้เลย

    - * - * - * - Start of Ubuntu install Command - * - * - * -
    ```
    for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
    ```

    # Add Docker's official GPG key:
    ```
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    ```

    # Add the repository to Apt sources:
    ```
    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    sudo docker run hello-world

    sudo groupadd docker

    sudo usermod -aG docker $USER

    newgrp docker

    docker run hello-world
    ```
    - * - * - * - End of Ubuntu Docker install Command - * - * - * -

