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


## src/config/config.prod.ts 配置文件注解

~~~shell
import { IConfigOptions } from "../types";

// 先从环境变量取配置
let config: IConfigOptions =  {
    version: '2.3',
    serve: {
    	// rap2服务器监听端口定义
        port: (process.env.EXPOSE_PORT && parseInt(process.env.EXPOSE_PORT)) || 8080,
    },
    // rap2 客户端连接KEY
    keys: ['sJLIgP0iJchKLz7pxlYHTOxmZRwdTjn4kVst7q7pOxEN41eqA4sV5pM3'],
    session: {
        key: 'rap2:sess',
    },
	// 数据库配置
    db: {
        dialect: 'mysql',
        host: process.env.MYSQL_URL || 'localhost',
        port: (process.env.MYSQL_PORT && parseInt(process.env.MYSQL_PORT)) || 3306,
        username: process.env.MYSQL_USERNAME || 'root',
        password: process.env.MYSQL_PASSWD || '',
        database: process.env.MYSQL_SCHEMA || 'rap',
        pool: {
            max: 80,
            min: 0,
            idle: 20000,
            acquire: 20000,
        },
        logging: false,
    },
    // redis数据库配置
    redis: {
        host: process.env.REDIS_URL || 'localhost',
        port: (process.env.REDIS_PORT && parseInt(process.env.REDIS_PORT)) || 6379
    },
    // 邮件发送配置
    mail: {
      host: 'smtp-mail.outlook.com',
      port: 587,
      secure: false,
      auth: {
          user: 'rap2_notify@outlook.com',
          pass: ''
      }
    },
    mailSender: 'rap2_notify@outlook.com',
}

export default config

~~~