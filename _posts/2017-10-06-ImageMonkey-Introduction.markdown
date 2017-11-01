---
layout: post
title:  "Let's create our own image dataset"
date:   2017-10-06 18:34:25
categories: general
image: /assets/article_images/2017-10-06-ImageMonkey-Introduction/taking_photo2.jpg
---

It's now a week since I posted about ImageMonkey on [reddit](https://www.reddit.com/r/MachineLearning/comments/731zwb/p_imagemonkey_a_public_open_source_image_database/). While the initial rush on ImageMonkey has slowed down and the load on the server stabilized again, it's time to reflect and plan the next development steps. 

# Thanks reddit #
First of all, I would like to thank the reddit community for all the great feedback and suggestions. It was my very first post on reddit and I wasn't expecting much, so I was really blown away to see that much load on the server. Hell, you guys even managed to take the server down temporarily!

>As it turned out there was a bug in the database connection pool handling which caused the number of open connections to grow rapidly until the point there were no connections left anymore. I am really glad that the *restart-the-application-every-10-minutes-cronjob-hack* "worked", otherwise I would have bitten myself in the ass for not doing any load testing beforehand. 

To give you some figures: In the first two days after the reddit post we got an incredible amount of **3002 image validations, 696 annotations and 20 donations**. 

Thanks, reddit!

# Goals #
<br>
> How do you want to convince people to label images? 

I think that's the question it all comes down to in the end. I am pretty sure there aren't many people out there that would use the words 'labeling images' and 'having fun' in one sentence. So in order to make the whole project work, we need to make the process of labeling images a painless and smooth as possible.

The following is a list of things that I would like to accomplish with ImageMonkey:


* **KISS** As I would assume there are not many people out there that actually have fun in labeling images, I think it's very important to make the process of labeling images as painless and fun as possible. If we make the labeling process too complicated people probably won't use it. <br><br>It would for sure be awesome to have a really fine granual labeled dataset, but in my opinion it would already be a huge accomplishment to identify some simple things (*apple*, *banana*, *smartphone*) reliable.

* **Contributer friendly** Another point that's really important for me is the possibility for users to contribute. As most of the backend stuff is written in Golang and not everybody knows Golang we should try to move as much "logic" a possible to config files. Scenes, Objects and Labels should be defined in (JSON like?) config files, so that users can easily create a pull request if they want to add something.

* **Tight feedback loop** I think it could be beneficial to have some sort of online playground where users can upload pictures and the system tries to classify them. Over time we should see that the model gets better and better in classifiying images. Such a feedback loop could motivate users to actually invest time in improving the dataset's quality, as they see a direct impact.

* **Open for contribution but closed for malicious modification** Everybody should be able to contribute (preferable without registration). Malicious attempts should be (automatically) detected and (if possible) prevented. If we can't detect it, we should at least be able to revert the malicious changes.

* **Easy wins/fail fast** As this is just a hobby project, we should focus on the "easy wins" first and try to rule out ideas, that need huge implementation effort but won't get us the desired results. I am usually not a fan of mockups, but I think here it could really save us some time in evaluating ideas.

* **"Do one thing philosophy"** I am a big fan of Unix' "Do one thing and do it well philosophy". I think with such a complex project it's pretty easy to "overdo things" in order to cover every possible use case. So it might be a good idea to figure out what we want in the end and break down the functionality in tiny apps/extensions with each of them fulfilling one specific purpose. I am afraid that if we put all the functionality in one application, that users will feel overwhelmed and don't know what they need to do. What I want to avoid is, that we make the base application so complicated and bloated that only "hardcore users" want to use it.

* **Aim for fast results** If we want to get some traction and recoginition we probably also need to attract users that are not technicians. So it could be beneficial to concentrate on some really "basic" image recognition first (with keeping the big picture in mind). For a normal user it's probably already pretty impresive if they can upload a picture of a dog and the dog gets marked. They most probably don't care if it's a labrador or a shepherd.

# What's next? #

There are a lot of things going on in our issues tracker. The following list should give you an overview about the most important actions we want to tackle.

* **Online Playground** As already mentioned, I think this one could add some playful character to the site and motivate people to participate. I recently added a proof of concept (you can try it out [here](https://imagemonkey.io/playground)). The model uses inception-v3 as base and was re-trained with the *dog*, *cat* and *apple* pictures in our dataset. The idea is to daily (at least as long as our dataset is so small) re-train the model to always serve the latest build. I haven't yet tried to performance test the implementation, so at that point it's really more a proof-of-concept ;)

* **Report Button** Just to be on the save side (with the law) we should add a button where users can report inappropriate content.

* **(Mockup-based) Evaluation** [@dobkeratops](https://github.com/dobkeratops) added some really nice ideas that we should consider implementing. But as most of them probably require some fundamental changes in the UI, the database layout and our config file structure, I think it could make sense to evaluate those ideas by either by implementing a proof-of-concept or some (UI) Mockups.

* **Statistics** Rich statistics could help guide people to do labelling that increases the breadth of the database.

* **Make project more contributer friendly** Currently the README is pretty detailed, which could scare off contributers. I think it could make sense to invest some time in making the "onboarding" more smoothly (e.q automate the manual steps; create a Dockerfile...)

* **Remove manual unlocking** Currently every uploaded donation gets unlocked manually in order to make sure that the uploaded content doesn't contain any sensitive material. While this is a good idea in ensuring that we don't accidentally become a hoster of sensitive material (nudity, racist content..) it simply doesn't scale. In order to keep ImageMonkey open and accessible for everybody we should start investigating early in methods to prevent malicious attempts (i.e nudity detection, blocking users with malicious intentions..)  

* **Logo** Every project needs a logo, right?

# Want to contribute? # 
First of all, I would like to thank [@dobkeratops](https://github.com/dobkeratops) for all the [awesome ideas and suggestions](https://github.com/bbernhard/imagemonkey-core/issues) - very much appreciated! It's always great to see such passion and contribution in Open Source projects - that's what Open Source is all about. 

As ImageMonkey and all it's parts are completely OpenSource, every contribution is highly appreciated. In case you want to check it out, here are some links:  

[https://github.com/bbernhard/imagemonkey-core](https://github.com/bbernhard/imagemonkey-core)

[https://github.com/bbernhard/imagemonkey-client](https://github.com/bbernhard/imagemonkey-client)

[https://github.com/bbernhard/imagemonkey-playground](https://github.com/bbernhard/imagemonkey-playground)

[https://github.com/bbernhard/imagemonkey-chrome-extension](https://github.com/bbernhard/imagemonkey-chrome-extension)

[https://github.com/bbernhard/imagemonkey-admin](https://github.com/bbernhard/imagemonkey-admin)







