```clojure
(ns profile.github
  (:require
    [profile.cover-letter     :refer [cover-letter]]
    [profile.resume           :refer [resume]]
    [profile.side-effects     :refer [email! update-cover-letter!]]
    [profile.accomplish-goals :refer [crush-interview! accept-offer!]]
    [profile.job-offers       :refer [clojure-or-rust-job-offers]]))

(def about-me
  {:name  "Chase Lambert"
   :email "chaselambert@gmail.com"
   :desc  "I am a self taught developer who has experience building full stack web apps.
           I am looking for a new role using Clojure/ClojureScript or Rust.
           I prefer remote but will consider relocation within the US.
           I have mainly focused on web development but am open to other projects as well"})

(def profile-links
  {:github   "https://github.com/chase-lambert"
   :linkedin "https://www.linkedin.com/in/chase-lambert/"})

(def profile (merge about-me profile-links))

(defn send-job-application [profile cover-letter resume job-offer]
  (let [app     (assoc profile :cover-letter cover-letter :resume resume)
        contact (:email job-offer)]
    (email! app contact)))

(defn find-new-job [job-offers]
  (doseq [{:keys [desc location offer-package] :as offer} job-offers
          :when (and (= desc "interesting challenge")
                     (= location :remote-or-enticing-offer-to-relocate)
                     (= offer-package :exciting))
          :let [letter (update-cover-letter! cover-letter)]]
    (send-job-application profile letter resume offer)
    (crush-interview!)
    (accept-offer!)))

(comment
  (find-new-job clojure-or-rust-job-offers))
```

or if you prefer statically typed languages...

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

        about: "I am a self taught developer who has experience building full stack web apps. \
                I am looking for a new role using Clojure/ClojureScript or Rust. \
                I prefer remote but will consider relocation within the US. \
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
                url:  "https://lessonplanner-rust.onrender.com/",
                repo: "https://github.com/chase-lambert/lesson_planner",
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
// Yes, this code compiles: https://github.com/chase-lambert/github_profile
```
