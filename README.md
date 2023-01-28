```rust
mod new_job;
mod profile;

use new_job::{find_new_job, MyNewJob};
use profile::{AboutMe, Project};

#[tokio::main]
async fn main() -> MyNewJob {
    println!("Hello, world!");

    let about_me = AboutMe {
        name: "Chase Lambert",

        about: "I am a self taught developer who has experience building full stack web apps.   \
                I have used Javascript with React (and Python with Flask and Django) but mostly \
                prefer using Clojure(script) and now Rust. \
                I am currently looking for full or part time work with Rust \
                I prefer remote but will consider relocation within the US  \
                I have mainly focused on web development but am open to other projects as well",

        skills: vec![
            "Rust",
            "Web Development",
            "Clojure(script)",
            "Python",
            "Javascript",
            "Typescript",
            "React",
            "Tailwind CSS",
            "HTMX",
        ],

        contact: "chaselambert@gmail.com",

        projects: vec![
            Project {
                name: "lessonplanner.ai",
                // Currently deployed on free tier so first load may be slow
                url:  "https://lessonplanner.onrender.com/",
                repo: "https://github.com/Chase-Lambert/lesson_planner",
                desc: "Full stack Rust app \
                       Backend uses Axum with a Postgres db \
                       Frontend uses Leptos with Tailwind CSS for styling \
                       Uses the OpenAI api to help teachers build lesson plans",
            },
            Project {
                name: "distance finder",
                // Currently deployed on free tier so first load may be slow
                url:  "https://distancefinder.onrender.com/",
                repo: "https://github.com/Chase-Lambert/distancefinder",
                desc: "Final project for Harvard's CS50 course \
                       Built using Python with Flask",
            },
        ],
    };

    println!("{about_me:#?}");

    let new_job = find_new_job().await?;

    Ok(new_job)
}
// Yes, this code compiles: https://github.com/Chase-Lambert/github_profile
```
