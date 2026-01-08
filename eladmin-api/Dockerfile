# 构建阶段：使用官方 Maven 镜像（国内可加速）
FROM maven:3.9.9-eclipse-temurin-8 AS builder

# 安装 git（部分项目需要）
RUN apt-get update && \
    apt-get install -y git && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY . .
# 如果你有阿里云 Maven 镜像 settings.xml，可以放进来加速依赖下载
COPY settings.xml /usr/share/maven/conf/settings.xml

# 跳过测试，强制生成 JAR 包
RUN mvn clean package -DskipTests -Dmaven.javadoc.skip=true -Dmaven.source.skip=true

# 运行阶段：只保留 JRE，体积小
FROM eclipse-temurin:8-jre

WORKDIR /app

# 自动找 eladmin-system/target 下的 jar 文件（不管叫什么名字）
COPY --from=builder /app/eladmin-system/target/*.jar app.jar

# 启动命令
CMD ["java", "-Dspring.profiles.active=prod", "-jar", "app.jar"]

