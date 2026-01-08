# 直接使用 nginx 托管你本地 build 好的 dist
FROM nginx:alpine

# 删除默认欢迎页
RUN rm -rf /usr/share/nginx/html/*

# 复制你本地构建好的 dist 文件夹（通过 docker build 时传入）
COPY dist/ /usr/share/nginx/html/

# 覆盖默认站点配置
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
