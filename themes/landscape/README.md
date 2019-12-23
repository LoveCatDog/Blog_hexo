# Landscape

A brand new default theme for [Hexo].

- [Preview](http://hexo.io/hexo-theme-landscape/)

## Installation

### Install

``` bash
$ git clone https://github.com/hexojs/hexo-theme-landscape.git themes/landscape
```

**Landscape requires Hexo 2.4 and above.** If you would like to enable the RSS, the [hexo-generate-feed] plugin is also required.

### Enable

Modify `theme` setting in `_config.yml` to `landscape`.

### Update

``` bash
cd themes/landscape
git pull
```

## Configuration

``` yml
# Header
menu:
  Home: /
  Archives: /archives
rss: /atom.xml

# Content
excerpt_link: Read More
fancybox: true

# Sidebar
sidebar: right
widgets:
- category
- tag
- tagcloud
- archives
- recent_posts

# Miscellaneous
google_analytics:
favicon: /favicon.png
twitter:
google_plus:
```

- **menu** - Navigation menu
- **rss** - RSS link
- **excerpt_link** - "Read More" link at the bottom of excerpted articles. `false` to hide the link.
- **fancybox** - Enable [Fancybox]
- **sidebar** - Sidebar style. You can choose `left`, `right`, `bottom` or `false`.
- **widgets** - Widgets displaying in sidebar
- **google_analytics** - Google Analytics ID
- **favicon** - Favicon path
- **twitter** - Twiiter ID
- **google_plus** - Google+ ID

## Features

### Fancybox

Landscape uses [Fancybox] to showcase your photos. You can use Markdown syntax or fancybox tag plugin to add your photos.

```
![img caption](img url)

{% fancybox img_url [img_thumbnail] [img_caption] %}
```

### Sidebar

You can put your sidebar in left side, right side or bottom of your site by editing `sidebar` setting.

Landscape provides 5 built-in widgets:

- category
- tag
- tagcloud
- archives
- recent_posts

All of them are enabled by default. You can edit them in `widget` setting.

## Development

### Requirements

- [Grunt] 0.4+
- Hexo 2.4+

### Grunt tasks

- **default** - Download [Fancybox] and [Font Awesome].
- **fontawesome** - Only download [Font Awesome].
- **fancybox** - Only download [Fancybox].
- **clean** - Clean temporarily files and downloaded files.

[Hexo]: https://hexo.io/
[Fancybox]: http://fancyapps.com/fancybox/
[Font Awesome]: http://fontawesome.io/
[Grunt]: http://gruntjs.com/
[hexo-generate-feed]: https://github.com/hexojs/hexo-generator-feed





今天又是New Day，记得前两年，自己情绪起伏波动比较大，总是容易多想，也不知道为啥，烦恼比较多，兴许是刚出学校，踏入社会 ，还未适应职场的勾心斗角、人之间的冷漠无情，苦头吃多了，变慢慢看开了。
2018年三月份，那时候是大二下半学期，跟着大部队去了北国，谁也不知道未来会如何，也不清楚自己的职业规划。第一来大城市的我，带着农村土乡土气的气息，对首都的敬畏无比强烈。期望着北国的雪，凛冽的雨，刺骨的风…正逢4月春，新的一年好兆头，春风吹醒了还在沉睡的大地，给我印象比较深刻的是柳絮，一簇簇的随风飘，像雪花、蒲公英…
近距离触摸着柳絮，肌肤的触感瞬间即化，大地馈赠给大地的礼物，除去了快节奏的生活。
充满童心的我还以为棉被的原材料就是漫天飞舞的柳絮。

一晃而过，大三实习期间到来，我们奔波在国都，面临着找实习岗位…
