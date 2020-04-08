---
title: Home
sections:
  - type: heroblock
    section_id: hero
    component: hero_block.html
    content: ''
  - type: contentblock
    title: About me
    section_id: about
    actions:
      - label: Gửi tin nhắn cho tôi
        url: /contact
    component: content_block.html
    content: >-
      Hi, mình là Phan Duy Lưu, hiện tại đang là AI engineer tại TMA solutions.
      Blog này là nơi tổng hợp 1 số bài viết thú vị trên mạng và những mẹo vặt
      mình tổng hợp lại trong quá trình làm việc, hi vọng có thể hữu ích với mọi
      người. Thân <3!
    image: /images/90048972_1873657586101849_8429022495499091968_o.jpg
  - type: postsblock
    title: Recent Posts
    section_id: recent-posts
    actions:
      - label: Xem tất cả bài viết
        url: blog/index.html
    component: posts_block.html
    num_posts_displayed: 6
menu:
  main:
    name: Home
    weight: 1
layout: home
---
