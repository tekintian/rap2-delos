# DIY编译使用步骤

RUN /bin/sh -c 'cd /tmp && npm install && npm install -g typescript && npm run build && mv ./dist/* /app/ && mv ./node_modules /app/ && rm -rf /tmp'

~~~shell
mkdir -p /home/wwwroot/
git clone https://github.com/tekintian/rap2-delos.git
cd rap2-delos
mkdir app
npm install && npm install -g typescript && npm run build && mv ./dist/* /home/wwwroot/rap2-delos/app/ && mv ./node_modules /home/wwwroot/rap2-delos/app/ && cp -a package.json /home/wwwroot/rap2-delos/app/package.json

~~~

创建rap2-delos  https://github.com/tekintian/rap2-delos

连接/home/wwwroot/rap2-delos/app目录到 rap2-delos 容器的 /app 目录即可
-v /home/wwwroot/rap2-delos/app:/app