# ACTIX-WEB


开发网站，可以使用[https://actix.rs/](actix-web)


## 安装
 

修改`Cargo.toml`的配置文件，在`dependencies`部分加上`axtix-web`


```config
[dependencies]
actix-web = "4"
```


## 实例


修改`main.rs`文件


```rust
use actix_web::{get, web, App, HttpServer, Responder};

#[get("/")]
async fn index() -> impl Responder {
  "Hello, World!"
}

#[get("/{name}")]
async fn hello(name: web::Path<String>) -> impl Responder {
  format!("Hello {}!", &name)
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
  HttpServer::new(|| App::new().service(index).service(hello))
    .bind(("127.0.0.1", 8080))?
    .run()
    .await
}
```


执行之后```cargo run```，可以在页面`127.0.0.1:8080`打开域名看到结果


