# docker/reverse-proxy/Dockerfile
# -------------------------------------------------
    FROM ubuntu:24.04

    LABEL org.opencontainers.image.title="Reverse-proxy Nginx"
    LABEL org.opencontainers.image.description="Nginx 1.26 sur Ubuntu 24.04 (noble)"
    LABEL maintainer="KevinJCode <you@example.com>"
    
    # ----- Paquets minimaux -----
    RUN apt-get update && \
        DEBIAN_FRONTEND=noninteractive \
        apt-get install -y --no-install-recommends \
            nginx=1.26.* \
            ca-certificates \
            curl \
            tzdata && \
        rm -rf /var/lib/apt/lists/*
    
    # ----- Configuration -----
    COPY nginx.conf /etc/nginx/nginx.conf
    COPY conf.d/    /etc/nginx/conf.d/
    
    # ----- Health-check -----
    HEALTHCHECK --interval=30s --timeout=3s \
      CMD curl -fs http://127.0.0.1/health || exit 1
    
    EXPOSE 80 443
    CMD ["nginx", "-g", "daemon off;"]
    