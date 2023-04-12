Just when you thought [Bevy](https://bevyengine.org/) couldn't get more ergonomic, Bvy shows up to change the game.
Is this a joke? You decide. Does it work? You can bet your Ass(etServer) it does.
Bvy shortens core Bevy ECS and some engine type names to a ... lets just say opinionated ... degree.
This is implemented with type aliases, which means this is 100% compatible with `bevy` types and plugins.
The author of this crate does not actually endorse using this crate over the actual [`bevy`](https://crates.io/crates/bevy) crate. Sometimes we just
build things because we can.

```rust
use bvy::*;

fn main() {
    App::new()
        .add_system(movement)
        .run();
}

fn setup(mut com: Com, ass: Ass) {
    com.spawn_bundle(OrthographicCamera::new_2d())
    com.spawn_bundle(SpriteBundle {
        texture: ass.load("player.png"),
        ..default()
    })
}

fn movement(time: R<Time>, mut transforms: Q<&mut Transform>) {
    for mut t in transforms.iter_mut() {
        t.translation.x += time.delta_seconds() * 10.0;
    }
}
```

## Changes
* `bevy::prelude::*` -> `bvy::*`
* `Query<&Transform>` -> `Q<&Transform>`
* `Res<Time>` -> `R<Time>`
* `ResMut<Assets<Mesh>>` -> `Rm<Assets<Mesh>>`
* `Commands` -> `Com`
* `AssetServer` -> `Ass`
* `Query<&Transform, With<Player>>` -> `Q<&Transform, W<Player>>`
* `Query<&Transform, Without<Player>>` -> `Q<&Transform, Wo<Player>>`
* `ParamSet<(Query<(&mut Transform, &Player)>, Query<&mut Transform>)>` -> `Ps<(Q<(&mut Transform, &Player)>, Q<&mut Transform>)>`
* `EventWriter<AppExit>` -> `Ew<AppExit>`
* `EventReader<AppExit>` -> `Er<AppExit>`
