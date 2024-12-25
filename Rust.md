# Rust

## 推荐内容

1. github：https://github.com/the-web3/chaineye-rust/tree/main/04-guess-game#readme
2. b站：https://www.bilibili.com/video/BV1hp4y1k7SV?spm_id_from=333.788.player.switch&vd_source=bba9e425afc6ec8309d4c32a37974100&p=6

## 基础内容

1. 猜数游戏

   crate库地址：https://crates.io/

第一版

```rust
use std::io;
fn main() {
    println!("Guess the number!");
    println!("Please input your guess.");

    let mut guess = String::new();
    io::stdin().read_line(&mut guess).expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```





# axum + 微信小程序案例

## 1. hello world

```rust
use axum::{
    routing::{get, post},
    http::StatusCode,
    Json, Router,
};
use tracing::info;


#[tokio::main]
async fn main() {
    // initialize tracing
    tracing_subscriber::fmt::init();

    // build our application with a route
    let app = Router::new()
        // `GET /` goes to `root`
        .route("/", get(root));
        // `POST /users` goes to `create_user`
        // .route("/users", post(create_user));

    // run our app with hyper, listening globally on port 3000
    let listener = tokio::net::TcpListener::bind("127.0.0.1:3000").await.unwrap();
    info!("listening on {}", listener.local_addr().unwrap());
    axum::serve(listener, app).await.unwrap();
}

// basic handler that responds with a static string
async fn root() -> &'static str {
    "Hello, World!"
}
```

```toml
[package]
name = "axum_learn"
version = "0.1.0"
edition = "2021"

[dependencies]
# "?" is shorter than ".unwrap()"
anyhow = "1"
# full features because of laziness
tokio = { version = "1", features = ["full"] }
# import the greatest framework
axum = "0.7"
tower = { version = "0.5.1", features = ["make", "util"] }
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }
serde = { version = "1.0", features = ["derive"] }
```

运行命令  `RUST_LOG=DEBUG cargo run` 运行命令可以看到log输出

### TODO

```
1. 引入sqlx
2. 使用evn，引入所有的配置信息
3. 搭建初步的信息
```

