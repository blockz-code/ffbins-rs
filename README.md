<center class="display: flex; align-items: center; justify-content: center; width: 100%; gap: 5px;">
<h1>ffbins-rs</h1>
<h3>Another ffmpeg wrapper</h3>
</center>

<center class="display: flex; align-items: center; justify-content: center; width: 100%; gap: 5px;">
    <span style="display: inline-block;">
        <a href="https://crates.io/crates/ffbins-rs">
            <img src="https://img.shields.io/crates/v/ffbins-rs?style=flat-square">
        </a>
    </span>
</center>

---

##### Supports on
+ **windows:** `ffmpeg`, `ffprobe`, `ffplay`
+ **linux:** `ffmpeg`, `ffprobe`, `ffplay`
+ **macos:** `ffmpeg`, `ffprobe`, `ffplay`
+ **android:** `ffmpeg`
 
##### Sources
+ **macos**   [luffyxddev/ffbins](https://github.com/luffyxddev/ffbins)
+ **linux**   [luffyxddev/ffbins](https://github.com/luffyxddev/ffbins)
+ **windows** [luffyxddev/ffbins](https://github.com/luffyxddev/ffbins)
+ **android** [luffyxddev/ffbins](https://github.com/luffyxddev/ffbins)

---

**Cargo.toml**
Not ready yet and not tested ... its made for plugin-rs

```toml
ffbins-rs = { version = "0.1.3" }
```



**Example**

```rust
use ffbins_rs::{Binary, FFbins, FFbinsCommands, Version};


fn main() -> anyhow::Result<()> {

    let cwd = dirs::data_local_dir().unwrap().join(env!("CARGO_PKG_NAME"));

    let mut ffbins = FFbins::new(Binary::FFmpeg, Version::V8_0_1, cwd.join("temp"), cwd.join("dest")).init().unwrap();

    ffbins.install(|state, current, total, percent| {

        println!("[{}] {}/{} {:.2}%", state.to_string(), current, total, percent);

    })?;


    FFbinsCommands::new(ffbins.binary())
        .command(cwd.join("data").join("1.mp4"))
        .output(cwd.join("data").join("1o.mp3"))
        .spawn(|key, value| {

            println!("{} : {}\n", key, value);

        })?;
    
    Ok(())

}
```
