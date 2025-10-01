---
layout: post
title: "Keeping a Widget Up to Date"
date: 2022-11-09 14:57:00
category: programming
tags: [swift, CS193P]
---


Use the following approaches to optimize the widget refreshed:  

1. Have the containing app prepare data for the widget in advance of when the widget needs it.  Use a shared group container to store the data.

2. Use background processing time in your app to keep shared data up to date.  For more information, see [Using background tasks to update your app](https://developer.apple.com/documentation/uikit/app_and_environment/scenes/preparing_your_ui_to_run_in_the_background/using_background_tasks_to_update_your_app).

3. Choose the most appropriate refresh policy for the information being shown, as described in the preceding section.  
4. Call `reloadTimelines(ofKind:)` only when information the widget is currently displaying changes.



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


