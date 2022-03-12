## My story as a web developer – mid-senior level

I'd like to thank every one of you who gave me feedback on the first part of my dev's journey. One of the questions that came up, is why am I writing all this? The answer is, that I'd like to encourage web developers, that are at the beginning of their journey, to dive in and fully submerge in this beautiful world of infinite possibilities. My articles on the topic aim to provide you with a couple of points of reference that I, myself, found useful and entertaining.

## Web dev's puberty - my first co-working efforts

After some time of playing with code on my own, I started to gain confidence in my skills. I started co-working with other people. It wasn't easy to find that many people that shared my passion for web development in the rural area where I lived. Usually, people didn't have a clue what I was talking about. Eventually, I got introduced to Ippy from [Netuxo Coop](https://netuxo.coop), who runs her small web development agency. She uses her contacts on the British and international activist scene to enable highly ethical NGOs to have a web presence and to pursue their online goals.

<figure>![CMS learning curve comparison - Drupal cliff](https://dev-to-uploads.s3.amazonaws.com/i/o8rbgjxx6gl3qz0xeum0.png)
<figcaption>Drupal's learning curve has even its own meme. What a legend!</figcaption></figure>

Netuxo focuses mainly on Drupal-based websites. This was a novelty for me. *Drupal's learning curve is legendary.* However, I enjoyed working with Ippy and Andrea(s). Even though I maintained my freelance status, I was working more and more exclusively for Netuxo. I was helping them with regular Drupal updates, designing websites and user interfaces, and then turning these into static HTML/CSS/JS prototypes and subsequently developing full-featured Drupal 8 themes.

It was then when I learnt about tooling. At first I was using my CSS pre-processor skills such as [SCSS/Sass](https://sass-lang.com/),[Compass](http://compass-style.org/) (does anybody still use it?) and [Less](http://lesscss.org/). It quickly became obvious, I needed some reliable way of compiling the source code that was more sustainable than running their command line default compilers. Some sort of tool that would enable me to write modern code, whilst making it readable for older browsers.

<figure>![Webpack configuration file](https://dev-to-uploads.s3.amazonaws.com/i/6qmbc1eto8xiwh57rlrx.jpg)
<figcaption>An example of a Webpack config file, enabling me to merge different partial configurations into one.</figcaption></figure>

I started off with a small desktop app called [Prepros](https://prepros.io/) – it's basically an app wrapper for Webpack and it does the job and does it well. The problem was, that I was the only one who could compile the code. Not an ideal situation in a collaborative context. The next obvious step was to learn [Webpack](https://webpack.js.org/). There is actually a couple of really good free courses at the [Webpack Academy](https://webpack.academy/), these got me started. Eventually, I settled on using [Laravel's Mix](https://laravel.com/docs/7.x/mix) for compiling front-end resources.

This opened up my possibilities because I could now use Javascript ES6. To start with I wasn't sure what I was doing and started mixing ES6 over ES5 without even realising I was doing that. Yet, it worked – thank you [Babel](https://babeljs.io/)! My ignorance was truly blissful. Around this time, I came across [Wes Bos aka @wesbos](https://twitter.com/wesbos) and a couple of his courses. At first, I bumped into [Javascript30](https://javascript30.com/). A great exercise course showing the new ES6 features on practical examples. At the same time, the [ES6.io Master Package](https://es6.io/) happened to be on sale. *Coincidence? I don't think so!* I jumped at the opportunity. This was a game-changer for me. Javascript suddenly felt *so much easier*. Wes is a brilliant teacher, he puts a lot of time into his courses and it shows. He can deliver the concept, not just the syntax and his examples and exercises are well-thought through. There are no confusing _foos_ and _bars_, but real-life situations using multimedia and user interaction. In short, Wes' courses are fun.

> {% podcast https://dev.to/syntax/javascript-tooling--004 %}
Wes teams up with [Scott Tolinski aka @stolinski](https://twitter.com/stolinski) and between them, they produce a podcast called [Syntax.fm](https://syntax.fm/). It's a great resource of knowledge about dev's technologies, technique's and also bbq tips. They are really entertaining – I highly recommend listening to them.

Whilst working with Netuxo I got to use the command-line interface (CLI) much more, as a lot of work was done remotely on their development servers. It also started to make sense to use some sort of Git branch-based workflow. Being a small team, we sometimes got away with forgetting to be meticulous about implementing it. 

There were periods of downtime with Netuxo, which usually coincided with the summer season as the rest of the team went away for their holidays. These periods would last for about two to three months. I had time for self-study. Working on my own projects was becoming more and more scarce, because I didn't chase any new leads, so I found myself more often participating in other people's projects during this time.

## [Knowledge Island](https://knowledgeisland.org/) – my mid-level graduation

There is one project I worked on during one of these (quieter) periods that I think is worth writing home about. I was recommended by Ippy to her ex-coworker, Joris. He was looking for someone to help him develop a new feature, for a web-based application, that helps young kids in the USA to fight the problem of childhood obesity. Joris was just too busy with other features, that he was happy to outsource this one to me.

The brief was to develop an online web application that would enable children to create personalised workout routines. They got to choose from a selection of 10 videos, each with different exercises. They can set the length for each exercise from three or four options and choose how many repetitions for each video. This would then generate a single video stream made up from a generic intro video, followed by the selected exercise videos (with the right amount of repetitions) and finished off with an encouraging outro video. All this would be saved using Ajax into the Joomla based main apps database. 

I had literally zero Joomla experience. After struggling with Drupal for what was by then about a year and a half, I made it clear with Joris, *"I'm happy to do the frontend part and even create the API interface but you will have to tie it all into Joomla yourself."* He agreed… phew!

I was a bit unsure about one particular aspect – Joris and his client Tony insisted on hosting the videos themselves. Prior to this gig, I had no experience of using the browser's video API. I always opted for some sort of 3rd party video player, whether it was Youtube, Vimeo or JW Video Player (when it was still in its infancy). I still said yes to the gig, thinking I'll just have to wing it. We compromised on using the [Video.js](https://videojs.com/) library to make it easier to deal with the stream part of the task.

And I winged it! I designed a responsive web app giving the users (kids) an intuitive interface based on drag&drop functionality. The result is smooth playing in-app generated video playlists that are optimised not only for various screen sizes but also for different bandwidths, as the kids often use mobile devices more than computers.

I can't really use that for my portfolio as it's behind a paywall and relies on copyrighted material for the video stream, but this was a significant project for me. It gave me the confidence that (with just an occasional consultation with the technical lead) I can tackle on my own and deliver on time, a project of this size and complexity. I've learnt that:

> *You shall face your fear of handling complex projects. Take them on, even if you don't know all the answers when starting. Analyze them, break them into smaller manageable chunks and deal with each chunk separately.*

## Moving on up…

In 2019, there was another significant length of downtime for me, in terms of my work with Netuxo. In the early summer, we finished an important project – an upgrade of a website providing access to NGOs and their lawyers to all British immigration-related court cases. More than 60,000 pages, some with many various taxonomies. I was responsible for the development of a large part of the Drupal 8 theme.

Once we launched, we all went for holidays in different parts of the world, thinking there will be more work from early autumn. As the summer was ending, there was bad news about projects being delayed, put on hold or some even cancelled. Our family finances were not ready for this kind of delay. I had not been chasing any of my own work leads for about two years by this time, so my funnel was pretty empty. I didn't actually want to do yet another artist's portfolio website anyway. There is no challenge for me doing that type of work, apart from explaining to the artist that their budget does not really allow for changing the way people navigate the internet and that they should instead focus on displaying their art and developing an online marketing strategy.

This is when I updated all my professional online accounts, wrote down my CV and sent it out to local contacts and then eventually to the world. It was time to up my game and work on a bigger project. I had been yearning to find my geek tribe - to be part of a bigger team, where the roles are more defined. But that is another story, one that I'm planning to publish soon.