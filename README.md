```rust
mod profile;
use profile::{AboutMe, Project};

fn main() {
    println!("Hello, world!");

    let about_me = AboutMe {
        name: "Chase Lambert",

        about: "I am a self taught developer who has experience building full stack web apps. I have used Javascript with React but mostly prefer using Clojure(script) and now Rust. I am currently looking for full or part time work (preferablly remote but will consider relocation within the US) with Rust. I have mainly focused on web development but am open to other projects as well.",

        skills: vec!["Rust", "Web Development", "Clojure(script)", "Javascript", "Typescript", "React", "Tailwind CSS", "HTMX"],

        contact: "chaselambert@gmail.com",

        projects: vec![
            Project { name: "lessonplanner.ai",
                      // Repo is currently private. Can allow access upon request.
                      repo: "https://github.com/Chase-Lambert/lesson_planner",
                      desc: "Full stack Rust app using Axum with a Postrgres db on the backend and Leptos on the frontend. Uses the OpenAI api to help teachers build lesson plans."
        },
            Project { name: "distance finder",
                      repo: "https://github.com/Chase-Lambert/distancefinder",
                      desc: "Final project for Harvard's CS50 course."},

    ]};
}
```
